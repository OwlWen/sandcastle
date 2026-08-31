# 理解清理层和完整 worktree 生命周期

`pruneStale()` 的两步清理（先 `git worktree prune` 清幽灵元数据，再扫描删孤儿目录）的顺序不可颠倒。`remove()` 通过路径反推 repoDir 而不接收参数，是因为调用方在清理阶段通常只持有 `worktreePath`。跨平台路径标准化通过三层保障（`normalizePath` 统一内部比较、`realPath` 解析符号链接、`normalize` 转回平台原生路径）解决了 Windows 分隔符不一致和符号链接误删两个真实 bug。

## Evidence
通过 quiz 验证了对 pruneStale 顺序依赖、remove 设计动机、符号链接数据丢失 bug 的理解。

## Implications
- 已建立对 WorktreeManager.ts 全部 539 行的完整心智模型
- 可以独立阅读调用方代码（createSandbox / SandboxFactory / interactive）
- 可以进入更高层模块或并发锁机制（ADR 0007）的学习
