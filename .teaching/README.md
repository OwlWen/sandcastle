# Sandcastle 交互式教学工作区 (Teaching Workspace)

本目录记录在 Sandcastle 代码库中的交互式教学课程、学习决策记录与参考资料。
AI Agent 在执行 `/mattpocock:teach` 技能时，必须遵循 [docs/agents/teach.md](../docs/agents/teach.md) 中定义的感知与路由协议。

---

## 目录结构规范

```text
.teaching/
├── README.md                  # 教学总览与全局看板（本文件）
├── assets/                    # 全局共享资产（样式表、通用脚本组件）
│   └── style.css
└── <topic-slug>/              # 主题工作区（按模块或领域划分）
    ├── MISSION.md             # 学习动机与目标
    ├── RESOURCES.md           # 一手参考资源与文献
    ├── NOTES.md               # 学习者偏好与导师笔记
    ├── lessons/               # 交互式课程 HTML（0001-*.html, 0002-*.html...）
    ├── learning-records/      # 学习决策记录（0001-*.md, 0002-*.md...）
    ├── reference/             # 压缩速查知识卡片与术语表（glossary.html...）
    └── assets/                # 主题私有资产（可选覆盖全局 assets）
```

---

## 学习主题看板 (Topic Dashboard)

| 主题 (Topic) | 状态 | 当前课时 | 最新学习记录 (ZPD) | 下一步规划 | 路径 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **`worktree-manager`** | 🟢 进行中 | 4 节课已完成 | `0004-sandbox-orchestration.md`<br>(已掌握 2×3 调度矩阵与双层 acquireUseRelease 编排) | 深入 `createSandbox.ts` 的 merge-to-head / ADR 0007 文件锁并发机制 | [worktree-manager/](./worktree-manager/) |

---

## 主题详情索引

### 1. `worktree-manager` (WorktreeManager 与 Sandbox 编排)
- **目标**: 深入理解 Sandcastle 如何利用 Git Worktree 实现隔离的工作区，以及 SandboxFactory 如何编排容器挂载与生命周期。
- **已完成课程**:
  - [第 1 课: 5 层架构全景图](./worktree-manager/lessons/0001-architecture-overview.html)
  - [第 2 课: create() 完整决策树与降级路径](./worktree-manager/lessons/0002-create-decision-flow.html)
  - [第 3 课: 清理层、跨平台路径陷阱与完整生命周期](./worktree-manager/lessons/0003-cleanup-layer.html)
  - [第 4 课: SandboxFactory 2×3 矩阵与双层 acquireUseRelease 编排](./worktree-manager/lessons/0004-sandbox-orchestration.html)
- **已建立学习记录 (ZPD 锚点)**:
  - `0001-prior-knowledge-baseline.md` (前置知识基准)
  - `0002-create-decision-tree.md` (create 决策树与先试后创)
  - `0003-cleanup-and-lifecycle.md` (prune 顺序与路径反推)
  - `0004-sandbox-orchestration.md` (编排矩阵与错误附着)
- **参考资料**:
  - [术语表速查](./worktree-manager/reference/glossary.html)
  - [一手知识源清单](./worktree-manager/RESOURCES.md)
