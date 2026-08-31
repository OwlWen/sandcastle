# Mission: 读懂 WorktreeManager.ts

## Why
搞懂 sandcastle 如何利用 git worktree 机制实现隔离的 agent 工作空间——理解 worktree 的创建、复用、冲突检测、清理的完整生命周期，以便能自信地阅读、调试和修改这个核心模块。

## Success looks like
- 能独立画出 `WorktreeManager.create()` 的完整决策流程图
- 能解释为什么需要 `NO_CONFIG_LOCK_FLAGS`、`fastForwardFromOrigin` 的每一个分支
- 能说清 branch 策略 vs merge-to-head 策略下 worktree 的不同行为
- 能看懂 Effect-TS 的 `Effect.gen` / `Effect.async` / `Effect.catchAll` 在这个模块中的用法

## Constraints
- 已有 TypeScript、git worktree、Effect-TS 的基础知识
- 以源码精读为主，不需要从零学习基础概念
- 中文教学

## Out of scope
- 不需要深入学习 Effect-TS 框架本身（只需理解本模块用到的模式）
- 不需要学习 sandcastle 的 agent provider 或 sandbox provider 层
