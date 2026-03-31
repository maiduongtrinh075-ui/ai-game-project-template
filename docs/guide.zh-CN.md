# 中文使用说明

这份模板的目标很简单: 让你可以把游戏拆成一个个模块, 然后让 AI 逐块扩写, 而不是每次都把整个项目搅乱。

它适合这些场景:
- 你已经有一个游戏原型, 想继续把某个系统做深
- 你希望 AI 只动战斗、UI、背包这类局部模块
- 你想让不同轮次的 AI 接力开发时更稳定

## 核心思路

这套模板把项目分成四层:

- 代码层: 真正运行的模块和资源
- 规则层: 告诉 AI 哪些地方能动, 哪些地方不要碰
- 设计层: 告诉 AI 每个系统当前做到哪一步, 将来准备怎么扩
- 任务层: 把需求变成小任务, 让 AI 每次都只吃一口

如果你只记一件事, 就记这个原则:

先给 AI 边界, 再给 AI 任务, 最后才让它改代码。

## 先看哪些文件

第一次使用时, 先看这些文件:

- `AI.md`: 项目总规则
- `.ai/context/project-overview.md`: 项目整体介绍
- `.ai/context/current-status.md`: 当前进度
- `.ai/context/boundaries.md`: 改动边界
- `docs/systems/`: 各模块设计说明
- `tasks/templates/`: 任务模板

如果你准备扩写战斗系统, 建议阅读顺序是:

1. `AI.md`
2. `.ai/context/boundaries.md`
3. `docs/systems/combat.md`
4. `src/gameplay/combat/README.md`
5. `tasks/in-progress/` 里当前任务文件

## 目录是怎么分工的

### `AI.md`

这是总入口。你可以把它理解成“AI 进项目后的操作说明”。

里面应该长期维护这些内容:
- 项目是什么
- 技术栈是什么
- 哪些区域已经稳定
- 哪些区域允许扩写
- 默认工作方式是什么

### `.ai/context/`

这是长期上下文, 用来减少 AI 每次都重新猜测项目状态。

推荐你持续维护:
- `project-overview.md`: 游戏是什么
- `current-status.md`: 当前做到哪
- `coding-rules.md`: 命名和代码约定
- `boundaries.md`: 不该动的地方
- `glossary.md`: 统一术语

### `.ai/workflows/`

这是任务执行套路。比如扩模块、修 bug、加功能, 都可以有固定步骤。

好处是你以后可以直接说:

“按 expand-module 工作流扩写 combat”

这样 AI 的行为会更稳定。

### `docs/systems/`

这里是每个模块的设计说明。它决定 AI 会不会把一个系统越改越乱。

每个模块文档建议至少写:
- 这个模块负责什么
- 当前已经实现了什么
- 下一步准备扩什么
- 输入是什么
- 输出是什么
- 哪些接口不能随便改

### `tasks/`

这里是你给 AI 的任务单。

不要只在聊天里说“帮我完善战斗系统”, 更稳的做法是把任务写成一个小文件, 例如:
- 这次目标是什么
- 哪些东西必须保持不变
- 允许改哪些目录
- 验收条件是什么

## 正确的使用方式

推荐你以后按下面这个流程和 AI 协作。

### 第一步: 先选一个模块

不要上来就说“完善整个游戏”。先选一个局部:
- combat
- dialogue
- inventory
- quests
- ui

### 第二步: 写一个小任务

在 `tasks/in-progress/` 下新建一个任务文件, 你可以从模板复制:
- `tasks/templates/module-expansion-task.md`
- `tasks/templates/feature-task.md`
- `tasks/templates/bug-task.md`

### 第三步: 给 AI 明确边界

你要让 AI 知道:
- 允许改哪些目录
- 不允许碰哪些系统
- 是否允许改数据结构
- 是否允许动存档

边界越明确, AI 越不容易扩写失控。

### 第四步: 让 AI 先做最小可运行版本

比如你想扩写战斗系统, 不要第一句就让它做“完整技能系统 + AI + 平衡 + 特效 + 动画”。

更稳的方式是:

1. 先加 3 个技能
2. 再加敌人简单行动逻辑
3. 再加 buff/debuff
4. 最后再做表现层和数值调整

### 第五步: 每轮都记录决策

如果本轮扩写改变了团队默认约定, 就把它写进:
- `.ai/memory/decisions.md`

如果本轮暴露了坑, 就写进:
- `.ai/memory/known-issues.md`

这样下一轮 AI 接手时不会反复踩同一个坑。

## 怎么给 AI 下指令更稳

下面是几种推荐说法。

### 扩写一个已有模块

```text
阅读 AI.md、.ai/context/boundaries.md、docs/systems/combat.md。
只扩写 combat 模块, 为玩家增加 3 个技能和敌人自动行动逻辑。
不要修改存档格式, 不要改全局事件名, 只允许修改 src/gameplay/combat 和相关 battle UI。
```

### 新增一个小功能

```text
按 add-feature 工作流处理 inventory 模块。
为背包增加物品分类筛选。
不要重构整个 UI, 保持现有数据结构兼容。
```

### 修一个局部 bug

```text
按 bugfix 工作流检查 quest 模块。
修复任务完成后奖励重复发放的问题。
不要修改存档结构, 优先做最小修复。
```

### 基于任务文件执行

```text
按 tasks/in-progress/example-combat-expansion.md 执行。
先读 docs/systems/combat.md, 再开始改代码。
```

## 不推荐的提法

这些说法太大, AI 很容易失控:

- “帮我完善整个游戏”
- “把系统都重构一下”
- “把战斗做完整”
- “把 UI 全部美化一下”

问题不在于 AI 听不懂, 而在于范围太大, 它会自己猜很多你没授权的东西。

## 一个实战示例

如果你现在有一个 Unity 或其他引擎做的原型, 战斗模块已经能“点一下扣血”, 想继续扩写, 可以这样做:

1. 先在 `docs/systems/combat.md` 写清楚当前能力
2. 在 `src/gameplay/combat/README.md` 写清楚模块职责
3. 在 `tasks/in-progress/` 新建一个扩写任务
4. 让 AI 只改 combat 目录和 battle UI
5. 本轮只做技能和敌人回合
6. 跑通后再开下一轮任务做状态效果

这个节奏比“一次做完整战斗系统”稳很多。

## 如果你是 Unity / C# / UGUI 项目

这套模板虽然是通用的, 但很容易映射到 Unity:

- `src/gameplay/` 可以对应 `Assets/Scripts/Gameplay/`
- `src/ui/` 可以对应 `Assets/Scripts/UI/`
- `assets/` 可以对应 Unity 里的 `Assets/` 资源层
- `docs/` 和 `.ai/` 建议保留在仓库根目录

关键点不是目录名字完全一致, 而是职责边界清楚:
- Gameplay 负责规则
- UI 负责显示和交互
- Core 负责公共基础设施
- Integration 负责模块连接

## 你可以立刻开始的最小做法

如果你不想一次整理太多, 先维护这几个文件就够了:

- `AI.md`
- `.ai/context/current-status.md`
- `.ai/context/boundaries.md`
- `docs/systems/combat.md`
- `src/gameplay/combat/README.md`
- `tasks/in-progress/` 下的一份任务文件

有了这几个文件, 你就已经能开始按模块让 AI 接力开发。

## 最后一个判断标准

如果你给 AI 的需求满足这三个条件, 通常就比较稳:

- 只针对一个模块
- 明确哪些地方不能动
- 验收标准是可测试的

比如:

“只扩写 combat, 不改存档, 增加 3 个技能, 战斗能正常结束。”

这种需求就很适合 AI。
