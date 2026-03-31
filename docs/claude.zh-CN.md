# Claude 版中文说明

这份说明是基于 Claude Code 常见项目组织方式整理的, 目的是让你把游戏项目变成“适合 Claude 接力扩写”的结构。

如果前一份 `AI.md` 模板更偏通用, 那这一份就是更接近很多人会给 Claude 准备的工程形态:
- 用 `CLAUDE.md` 作为总入口
- 用 `.claude/` 存放命令、设置和工作流
- 用模块文档约束 Claude 每次只扩写一个功能块

## 它和通用模板的关系

你可以把两者理解成:

- `AI.md` 版: 更通用, 不绑定具体模型习惯
- `CLAUDE.md` 版: 更贴近 Claude Code 社区常见写法

两种方法本质一样, 都是在做三件事:
- 给 AI 规则
- 给 AI 上下文
- 给 AI 明确边界

所以它不是“Claude 才能用”, 而是“按 Claude 常见方式组织出来, 让 Claude 更容易接手”。

## 推荐目录

下面是一个适合 Claude 的游戏项目结构:

```text
game_project/
├─ CLAUDE.md
├─ README.md
├─ .claude/
│  ├─ settings.json
│  ├─ commands/
│  │  ├─ expand-module.md
│  │  ├─ add-feature.md
│  │  └─ bugfix.md
│  └─ memory/
│     ├─ decisions.md
│     └─ known-issues.md
├─ docs/
│  ├─ architecture/
│  ├─ systems/
│  ├─ content/
│  └─ decisions/
├─ tasks/
│  ├─ in-progress/
│  └─ templates/
├─ src/
│  ├─ core/
│  ├─ gameplay/
│  ├─ ui/
│  ├─ data/
│  └─ integration/
└─ assets/
```

## `CLAUDE.md` 应该写什么

`CLAUDE.md` 是总入口, 很像“Claude 进入项目后第一眼该看的说明书”。

建议长期维护这些内容:
- 项目目标
- 技术栈
- 模块边界
- 稳定区域和可扩写区域
- 默认工作方式
- 哪些文件优先读

一个好的 `CLAUDE.md` 应该让 Claude 一进项目就知道:

- 这是个什么游戏
- 我这轮该优先看什么
- 哪些地方不能乱动
- 修改后需要补什么文档

## `.claude/commands/` 是干什么的

这里可以放你常用的任务说明模板。

例如:
- `expand-module.md`: 扩写一个已有模块
- `add-feature.md`: 给一个已有模块加功能
- `bugfix.md`: 修一个局部 bug

这样你以后可以直接对 Claude 说:

```text
按 .claude/commands/expand-module.md 的方式扩写 combat 模块
```

这种说法通常比“帮我完善战斗系统”更稳。

## `.claude/memory/` 是干什么的

这是给后续轮次保留记忆的地方。

推荐至少放:
- `decisions.md`: 记录长期决策
- `known-issues.md`: 记录已知坑点

当你多轮使用 Claude 做游戏时, 这个目录会很有价值, 因为它能减少模型反复走弯路。

## 怎么让 Claude 按模块扩写游戏

这里是最关键的部分。

### 1. 每次只点一个模块

不要让 Claude 同时碰:
- 战斗
- 背包
- 任务
- UI
- 存档

更稳的方式是一次只做一个:
- 只扩写 combat
- 只扩写 inventory
- 只改 battle UI

### 2. 先给边界, 再给目标

比如这样说:

```text
阅读 CLAUDE.md 和 docs/systems/combat.md。
只扩写 combat 模块, 增加 3 个技能和敌人自动行动逻辑。
不要修改存档格式, 不要修改全局事件名, 只允许改 src/gameplay/combat 和相关 battle UI。
```

这类指令非常适合 Claude。

### 3. 任务文件比口头描述更稳

推荐你把需求写进 `tasks/in-progress/` 下的任务文件, 然后直接让 Claude 按任务执行。

例如:

```text
按 tasks/in-progress/example-combat-expansion.md 执行。
先读 CLAUDE.md, 再读 docs/systems/combat.md。
```

### 4. 先做最小扩写, 再开下一轮

不建议一轮里做太多。更推荐这种节奏:

1. 先加 3 个技能
2. 再加敌人简单 AI
3. 再加状态效果
4. 再做表现层和数值调整

这样 Claude 更容易稳定输出。

## 一个适合 Claude 的提需求公式

你以后可以直接套这个模板:

```text
阅读 CLAUDE.md、相关模块文档和任务文件。
目标: <这次要扩写什么>
只允许修改: <允许改的目录>
不要修改: <不能动的系统或接口>
验收标准: <功能完成后要满足什么>
```

例如:

```text
阅读 CLAUDE.md、docs/systems/inventory.md、tasks/in-progress/inventory-filter.md。
目标: 为 inventory 模块增加分类筛选。
只允许修改: src/gameplay/inventory, src/ui/inventory。
不要修改: 存档结构、道具 ID 格式。
验收标准: 玩家可以按类别过滤物品, 原有添加和删除逻辑不受影响。
```

## 哪些写法最容易让 Claude 失控

下面这些说法范围太大:

- “帮我把游戏整体完善一下”
- “把战斗系统做完整”
- “顺便把 UI 和存档也整理一下”
- “觉得哪里不合理就一起改掉”

Claude 不一定做不到, 但它会被迫补很多你没明确授权的假设。

## 如果你是 Unity / C# / UGUI 项目

Claude 版结构也完全能套在 Unity 项目里:

- `src/gameplay/` 对应 `Assets/Scripts/Gameplay/`
- `src/ui/` 对应 `Assets/Scripts/UI/`
- `assets/` 对应 Unity 的资源层
- `CLAUDE.md`、`.claude/`、`docs/`、`tasks/` 放仓库根目录

关键不是目录名, 而是职责:
- Gameplay 负责规则
- UI 负责表现和交互
- Core 负责基础设施
- Integration 负责模块连接

## 这份仓库里已经给你的 Claude 示例

我还补了一组 Claude 风格的示例文件, 你可以直接看:

- `templates/claude/CLAUDE.md`
- `templates/claude/.claude/settings.json`
- `templates/claude/.claude/commands/expand-module.md`
- `templates/claude/.claude/commands/add-feature.md`
- `templates/claude/.claude/commands/bugfix.md`

你可以把这些文件复制到你的真实项目里, 再按项目实际情况改掉占位内容。

## 最后一个判断标准

如果你的需求同时满足这三点, Claude 通常就很好用:
- 只针对一个模块
- 明确说了不能动什么
- 验收条件可以被检查

例如:

“只扩写 combat, 不改存档, 增加 3 个技能, 战斗能正常结束。”

这种就是非常适合 Claude 接手的需求。
