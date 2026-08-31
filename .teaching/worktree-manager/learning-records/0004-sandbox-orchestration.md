# SandboxFactory 通过 2×3 调度矩阵编排 worktree 生命周期

`SandboxFactory.withSandbox()` 的 692 行代码是一个 2 维调度：sandbox provider（none / isolated / bind-mount）× branch strategy（head / merge-to-head / branch）。head 策略不创建 worktree；其余组合都走 pruneAndCreate → use → cleanupWorktree 生命周期。

核心模式是双层嵌套的 `Effect.acquireUseRelease`——外层管 worktree 生命周期，内层管 sandbox handle 生命周期，确保即使中间步骤（copy、hook）失败也能正确清理。`attachPreservedPath` 通过闭包变量在 release 阶段和 mapError 之间传递保留路径信息。

## Evidence
通过 quiz 验证了对双层 acquireUseRelease 必要性、错误附着机制、isolated 不支持 head 的类型级原因的理解。

## Implications
- 已建立从 WorktreeManager（工具层）到 SandboxFactory（编排层）的完整心智模型
- 能独立阅读 run() 和 createSandbox() 的代码——它们是 SandboxFactory 的上层调用者
- 理解了 Effect.acquireUseRelease 模式可以扩展到分析 sandcastle 其他资源管理场景
