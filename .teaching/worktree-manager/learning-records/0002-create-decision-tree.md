# 理解 create() 的决策树结构

`create()` 函数（L291-428）的 138 行代码按"有 branch vs 无 branch"分成两条主路径，其中 branch 路径包含碰撞检测、managed/unmanaged 区分、clean/dirty 分流、以及"先试后创"降级逻辑。`fastForwardFromOrigin()` 的 `never` 错误通道是 ADR 0003 "非致命"原则的类型级保证。

## Evidence
通过决策流程图走读和 quiz 验证了对每条路径的理解。

## Implications
- 下一步可以进入清理层（`pruneStale` / `remove`）
- 已理解 `Effect.either` 和 `catchAll` 在错误降级中的不同用法——`either` 用于可预期的非致命失败，`catchAll` 用于按错误消息做条件降级
