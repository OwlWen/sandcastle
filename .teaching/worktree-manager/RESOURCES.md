# WorktreeManager.ts 学习资源

## Knowledge

- [Git Worktree 官方文档](https://git-scm.com/docs/git-worktree)
  git worktree 的权威参考。核心限制：同一分支不能在两个 worktree 同时 checkout。用于理解 sandcastle 碰撞检测逻辑。
- [ADR 0003: Reuse existing worktree by default](file:///Users/Owen/Projects/ai/sandcastle/.worktrees/main/docs/adr/0003-reuse-worktree-by-default.md)
  解释了 worktree 复用策略的设计决策——clean 时 fast-forward，dirty 时带警告复用，diverged 时保持不动。
- [ADR 0018: Fork is session only](file:///Users/Owen/Projects/ai/sandcastle/.worktrees/main/docs/adr/0018-fork-is-session-only.md)
  解释了 `generateTempBranchName` 需要随机后缀的原因——并发 fork 可能在同一秒内碰撞。
- [CONTEXT.md — Sandcastle 领域术语](file:///Users/Owen/Projects/ai/sandcastle/.worktrees/main/CONTEXT.md)
  所有 sandcastle 领域术语的定义。特别关注 Worktree、Branch strategy、Source branch、Target branch。
- [Effect-TS 文档 — Effect.gen](https://effect.website/docs/effect/essentials/using-generators)
  Effect.gen 的 generator 语法用法。用于理解 `yield*` 在 Effect 中的含义。
- [源码: WorktreeManager.ts](file:///Users/Owen/Projects/ai/sandcastle/.worktrees/main/src/WorktreeManager.ts)
  本次学习的主源文件。539 行，包含 create / remove / pruneStale 三个核心操作。
- [源码: errors.ts](file:///Users/Owen/Projects/ai/sandcastle/.worktrees/main/src/errors.ts)
  WorktreeError 和 WorktreeTimeoutError 的定义。基于 Effect 的 Data.TaggedError。

## Gaps

- Effect-TS 的 `Effect.async` 具体行为（resume 回调的语义）——需要找到更好的一手文档
