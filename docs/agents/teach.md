# Teaching in Sandcastle

How engineering agents should interact with and contribute to the teaching workspace in this repository when the user invokes the `/mattpocock:teach` skill.

---

## 1. 核心定位与原则

在本项目中，所有由 `/mattpocock:teach` 生成的教学资料均按主题隔离在 `.teaching/<topic-slug>/` 目录下，并在 `.teaching/README.md` 统一维护全局看板。

**严禁将教学文件直接散落到项目根目录。** 必须严格遵循本指南定义的 4 步工作流，确保不同会话中的 Agent 能够无缝感知与衔接既有学习进度。

---

## 2. 教学工作区目录规范

```text
.teaching/
├── README.md                  # 全局学习进度与主题索引看板（所有 Agent 的第一入口）
├── assets/                    # 全局共享静态资产（style.css 等）
└── <topic-slug>/              # 主题工作区（例如 worktree-manager, prompt-engine）
    ├── MISSION.md             # 学习动机与边界定义
    ├── RESOURCES.md           # 一手高信任资源文献
    ├── NOTES.md               # 学习者背景与偏好记录
    ├── lessons/               # 交互式课程 HTML（必须按 0001-slug.html 递增）
    ├── learning-records/      # 学习决策记录（必须按 0001-slug.md 递增，用于锚定 ZPD）
    ├── reference/             # 压缩速查参考（glossary.html 等）
    └── assets/                # 主题私有资产（可选）
```

---

## 3. Agent 4 步工作流协议 (The 4-Step Protocol)

当收到 `/mattpocock:teach <topic>` 或继续教学的指令时，Agent 必须按顺序执行以下步骤：

### 步骤 1：主题路由与发现 (Topic Discovery & Routing)
1. **读取全局看板**：首先读取 `.teaching/README.md`。
2. **匹配已有主题**：
   - 若用户提及的主题已在 `.teaching/<topic-slug>/` 存在（例如 `WorktreeManager` 对应 `worktree-manager`），则锁定该主题目录。
   - 若用户未指定具体主题但当前正在学习某一模块，优先复用该模块对应的已存在主题。
   - 若为全新主题，在 `.teaching/<new-topic-slug>/` 初始化目录并先询问用户的学习动机以生成 `MISSION.md`。

### 步骤 2：状态与 ZPD 检索 (State & ZPD Retrieval)
在进入目标主题工作区后，Agent 必须在生成任何新内容前读取以下状态：
1. **检索最新认知边界**：读取 `.teaching/<topic>/learning-records/` 下的所有文件，找出最大序号的记录，以此判断用户的**最近发展区 (Zone of Proximal Development, ZPD)**，严禁重新向用户提问已记录的已知知识。
2. **计算课时序号**：扫描 `.teaching/<topic>/lessons/` 目录，找出当前最大课时编号（如已有 `0004-*.html`，则下一节课**必须**命名为 `0005-*.html`）。
3. **查阅动机与资源**：读取 `MISSION.md`、`RESOURCES.md` 与 `NOTES.md`，确保后续教学与既定目标严格对齐。

### 步骤 3：课程与记录产出规范 (Asset Authoring)
1. **统一中文交互与文档**：所有文档、代码注释与课程内容强制使用中文。
2. **美观与样式共享**：
   - 课程 HTML 必须在 `<head>` 中引入样式：`<link rel="stylesheet" href="../assets/style.css">`。
   - 保持排版优雅（包含层级图、决策树、折叠卡片与交互式 Quiz 检验）。
3. **编写 Learning Record**：在用户理解关键决策后，创建 `.teaching/<topic>/learning-records/NNNN-<slug>.md`，简明记录所掌握的知识点及对后续学习的影响。
4. **浏览器即时打开**：生成课程后，主动在终端运行 `open .teaching/<topic>/lessons/NNNN-<slug>.html` 为用户打开页面。

### 步骤 4：看板同步回写 (Dashboard Synchronization)
在完成课程或学习记录产出后，Agent **必须**更新 `.teaching/README.md`：
- 更新表格中该主题的「当前课时」与「最新学习记录 (ZPD)」；
- 更新「下一步规划」；
- 在主题详情索引中追加新课程与新记录的链接。

---

## 4. 示例：如何确定下一课编号

若 `.teaching/worktree-manager/` 下已有：
- `lessons/0001-architecture-overview.html`
- `lessons/0002-create-decision-flow.html`
- `lessons/0003-cleanup-layer.html`
- `lessons/0004-sandbox-orchestration.html`

Agent 在生成下一课时：
- 新课文件名必须为：`lessons/0005-<dash-case-name>.html`
- 新学习记录必须为：`learning-records/0005-<dash-case-name>.md`
- 并在 `.teaching/README.md` 中将当前状态更新为 `5 节课已完成`。
