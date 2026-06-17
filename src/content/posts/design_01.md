---
title: "墨染仙途开发日志_01"
published: 2026-06-09
pinned: true
description: "AI开发卡牌游戏墨染仙途日志"
image: ./images/fengmian_1.png
tags: ["示例", "开发日志", "墨染仙途"]
category: "开发日志"
author: "AllenW"
draft: false
---

<a id="youtube"></a>
# 开发日志_01

## 开发信息

引擎版本：Cocos Creator 3.8.8。

开发语言：TypeScript。

游戏类型：Roguelike 卡牌构建（DBG）

游戏题材：修仙

## 开发演示

![工具说明](./images/caozuojietu_1.gif)

基于AI构建的大部分功能已经完善，能够进行绝大部分的操作，包括路线图，手牌牌库，弃牌堆，BUFF展示等，目前数值体系已经配置完毕，正在补全美术素材以及制作游戏测试Skill进行压测。研发总耗时7d。

1.游戏由AI辅助开发，基于Cocos Creator 3.8引擎，采用Typescript语言；

2.美术资源均有image_2辅助出图，并采用PS等专业美术软件进行后期修改；

3.角色骨骼网格动画由开源AI工具进行裁图，并采用龙骨动画软件进行动画制作；

4.游戏音效均由商业软件DSP Motion进行自定义设计；

5.游戏BGM音乐由AI软件SUNO进行生产；

6.游戏数值配置由AI产出html模拟器，通过本地配置并AI模拟测试高压轮数后导出json文件，直接导入引擎后生效

7.游戏内系统架构均由自己设计，其中包括UI控件的控制，不同设备的分辨率自适应，以及配置表文件的设计

后续计划：目前已经跑通了无尽模式，后续计划将补充世界观，加入关卡增加游戏深度。

## 开发思路

游戏定位为游戏类型：Roguelike 卡牌构建游戏。需要先将基本信息告知AI，让AI先对项目的开发环境有一个基本定位，并且在开发中为了保证开发过程的可控性采用了MCP工具进行协作。

```yaml
【角色设定与系统环境】

你现在是一位资深的 Cocos Creator 3.8.8 游戏前端主程，精通 TypeScript 以及组件化架构设计。
我们当前正在通过 MCP 工具协作，你可以直接读取、创建和修改我的工作区文件。

【项目目标】

请帮我从零开发一款类似《杀戮尖塔》（Slay the Spire）的 Roguelike 卡牌构建（DBG）小游戏 Demo。
游戏采用东方的修仙背景。

【技术栈与编码规范】

引擎版本：Cocos Creator 3.8.8。

开发语言：TypeScript（开启严格模式）。

架构规范：

严格使用 Cocos 3.8 的装饰器语法（@ccclass('xxx'), @property）。

数据与表现分离：核心战斗数据和逻辑独立为纯 TS 类，UI 表现层继承自 Component。

解耦：统一使用全局事件总线（EventTarget 或自定义 EventManager）处理跨模块通信。

【核心系统需求】

卡牌系统 (Card System)

牌库流转：抽牌堆（Draw Pile） -> 手牌（Hand） -> 弃牌堆（Discard Pile）。（暂不考虑消耗堆）

卡牌数据：ID、名称、能量消耗（Cost）、类型（攻击/技能）、基础数值、卡牌描述。

战斗状态机 (Battle State Machine)

战斗流程：玩家回合开始（抽牌、重置能量） -> 玩家出牌阶段 -> 玩家回合结束 -> 敌方回合（执行意图） -> 结算。

实体系统 (Entity System)

包含玩家（Player）和敌人（Enemy）的基类。

核心属性：当前血量（HP）、最大血量（Max HP）、格挡值（Block，回合开始时清零）、能量（Energy）。

【MCP 执行步骤计划】

为了保证代码质量和项目结构的清晰，请你严格按照以下四个阶段分步执行。
规则：每完成一个阶段的任务，请向我汇报已创建/修改的文件列表，然后必须暂停，等待我回复“继续”后，才能进入下一阶段。

第一阶段：基础架构与数据模型

在 assets/Scripts/ 目录下创建标准的子目录结构：Models, Managers, UI, Events, Utils。

编写全局事件总线 EventManager.ts 单例，并定义所有关键事件常量（如：回合切换、卡牌打出、血量变化）。

定义核心接口与纯数据模型（非 Component）：CardData.ts（卡牌数据） 和 EntityData.ts（实体数据，包含受伤、获得格挡的逻辑）。
[执行完此阶段请暂停并向我汇报]

第二阶段：核心管理器与状态机

编写 GameManager.ts 控制游戏全局状态初始化。

编写 CardManager.ts 处理牌堆洗牌、抽N张牌、打出卡牌、弃牌逻辑。

编写 BattleManager.ts 实现回合制状态机（使用 State 模式或 Switch/Case），管理玩家回合与敌人回合的切换。
[执行完此阶段请暂停并向我汇报]

第三阶段：UI 表现层组件

编写 CardUI.ts 组件：处理单张卡牌的 UI 渲染。实现基于 Node.EventType.TOUCH_MOVE 等事件的卡牌拖拽逻辑，以及释放时的目标检测与打出判定。

编写 BattleUI.ts 组件：控制玩家/敌人血条更新、当前能量值显示、以及“结束回合”按钮的事件绑定。

提供一份简要的说明，指导我需要在 Cocos 编辑器中如何搭建节点树（Node Tree）并挂载这些脚本。
[执行完此阶段请暂停并向我汇报]

第四阶段：卡牌效果实现与简易 AI

实现 2 张基础卡牌的具体效果代码：

“打击”（Strike）：消耗 1 能量，对目标造成 6 点伤害。

“防御”（Defend）：消耗 1 能量，获得 5 点格挡。

实现一个最基础的敌人 AI：每回合固定对玩家造成 5 点伤害。

将上述逻辑接入 BattleManager 以完成战斗闭环。
[最终完成汇报]

现在，请开始执行第一阶段的任务，生成代码并直接通过 MCP 写入到我的工作区中。
```

---

上一阶段的prompt已经构建之后，基本已经有一个可以满足基本需求的demo，但是为了之后的可视化需求，可以先搭建一个简单的UI框架，方便验证基本功能。

```yaml
【当前阶段目标】

基于第一至第三阶段已完成的核心逻辑（管理器、数据模型、UI 脚本），我现在需要你直接介入 Cocos Creator 场景与预制体 (Prefab) 的创建和绑定。
我们的目标是：通过 MCP 工具（或通过生成对应的 .fire / .prefab 文件数据，或提供极其详细的代码生成节点方案），实现当前基础功能的可视化，使游戏能够初步运行并展示 UI。

【任务拆解与执行步骤】

请按照以下步骤，帮我实现 Cocos Editor 场景树的自动化搭建或提供精准的挂载代码。
规则：你可以编写一个可以在 Cocos 编辑器运行时执行的临时脚手架脚本 (SetupTool.ts) 来动态生成这些节点，或者告诉我如何通过引擎 API 自动化构建场景。

第一步：编写场景/UI初始化脚本 (UISetupTool.ts)

请在 assets/Scripts/Utils 目录下创建一个名为 UISetupTool.ts 的脚本。

该脚本需要暴露一个 @property 绑定的入口方法（例如一个可以通过编辑器按钮触发的 setupScene() 方法，或者在 onLoad 中根据标记判断是否初始化）。

脚本内容需完全按照之前汇报的节点树结构进行代码动态生成：

创建 GameRoot 节点并挂载到 Canvas 下。

创建 Managers 节点，并依次挂载并引用 GameManager, CardManager, BattleManager 组件。

创建 BattleLayer 节点，挂载 BattleUI 组件。

在 BattleLayer 下创建 PlayerPanel、EnemyPanel 及相应的文本标签（使用 Cocos 默认的 Label 组件）。

创建 PhaseLabel (回合状态指示)、EndTurnButton (按钮组件) 和 PlayTargetArea (用于接收拖拽释放判定的空节点或带半透明 Sprite 的节点)。

创建 HandLayer 节点。

第二步：动态生成卡牌预制体 (CardPrefabGenerator.ts)

编写一个简易的代码逻辑，在运行时动态生成 CardItem 的 UI 节点结构。

该节点需要包含：背景框 (Sprite)、NameLabel、CostLabel、TypeLabel、ValueLabel、DescriptionLabel。

自动将 CardUI 组件挂载到该节点，并通过代码将对应的 Label 节点赋值给 CardUI 的 @property。

提供一个测试接口：在 GameManager.start() 或测试按钮中，实例化 3-5 张测试卡牌并挂载到 HandLayer。

第三步：组件绑定与初始化连接

在 UISetupTool.ts 中，使用代码实现组件间的引用绑定：

将生成的标签、按钮、PlayTargetArea 赋值给 BattleUI 的对应属性。

将 BattleManager 和 CardManager 赋值给需要的 UI 或 GameManager。

编写一份极其简短的“人工操作指南”，告诉我如何运行这个 UISetupTool.ts（例如：挂载到 Canvas 上，点击自定义的 Inspector 按钮，或者直接运行游戏触发）。

【输出要求】

不要输出任何场景树层级文本，我需要你直接输出 TypeScript 代码，这些代码要能直接通过 Cocos API 创建出这些节点并完成组件绑定。

请直接使用 new Node() 和 node.addComponent() 等引擎 API。

请确保代码中包含了基础的 UI 排版逻辑（例如简单的 setPosition 或添加 Layout 组件），以便运行时 UI 不会全部重叠在屏幕中心 (0,0) 的位置。

执行完成后，请汇报生成的脚本文件，并告诉我如何触发执行。
```

---

之前的框架只有基本的卡牌效果，为了规范化卡牌效果，为后续的开发能够有更高的自由度，将卡牌效果用配置表的模式进行开发。

```yaml
【当前阶段目标】

基于已有的关卡系统和战斗状态机，我现在需要对卡牌系统进行彻底的重构与升级。
目标是：实现卡牌数据驱动，通过 CardConfig.json 读取卡牌信息；并建立一套可扩展的多重效果解析系统（Effect System）与基础 Buff 系统，以支持复杂多样的卡牌行为。

【核心需求与设计规范】

1. 卡牌配置表 (CardConfig.json)

在 assets/resources/configs/ 下新增 CardConfig.json。

核心设计：每张卡牌需要支持“多重效果”。例如一张卡既能造成伤害，又能上 Buff，还能抽牌。

字段示例：id, name, cost, type (Attack/Skill/Power), target (SingleEnemy/AllEnemies/Self), description。

关键字段 effects：一个数组，定义该卡牌触发的一系列原子效果。

例如：[{"type": "Damage", "value": 6}, {"type": "ApplyBuff", "buffId": "vulnerable", "value": 2}]。

2. 原子效果处理器 (EffectProcessor)

编写 EffectProcessor.ts（或类似的管理类），负责解析和执行 JSON 中定义的 effects 数组。

需要支持的基础原子效果类型：

Damage (造成伤害)

Block (获得格挡)

DrawCard (抽牌)

Heal (回血)

ApplyBuff (施加状态)

3. 基础状态/Buff 系统 (Buff System)

扩展 EntityData（实体类），为其添加一个状态列表（如 Map<string, number> 记录 Buff 及其层数）。

实现 2 个基础 Buff 的结算逻辑（为了验证系统）：

Strength (力量)：增加攻击卡牌造成的伤害。

Vulnerable (易伤)：受到的伤害增加 50%。

4. 动态打牌逻辑重构

修改 CardManager.playCard 和 BattleManager：打出卡牌时，不再硬编码“打击/防御”的逻辑，而是将卡牌的 effects 数组交由 EffectProcessor 遍历执行，并传入正确的施法者 (Player) 和目标 (Target)。

【任务拆解与执行步骤】

请严格按照以下三个阶段分步执行，并在一阶段完成后暂停等待我的指令。

第一阶段：配置表生成与加载

创建 CardConfig.json，在其中设计 4 张具有代表性的测试卡牌：

普通攻击（单体伤害）

普通防御（单体格挡）

痛击（造成伤害 + 给予2层易伤）

肌肉记忆（0费，获得2层力量 + 抽1张牌）

更新已有的 ConfigManager.ts，增加对 CardConfig.json 的异步加载和解析逻辑，提供 getCardConfigById 方法。

更新 CardData.ts 接口，使其与 JSON 结构对齐。
[执行完此阶段请暂停并向我汇报，等待我确认 JSON 结构]

第二阶段：Buff 系统与效果解析器

修改 EntityData.ts，加入基础的 Buff 管理方法（addBuff, getBuffStack）。并在其 takeDamage 等方法中，接入“易伤”和“力量”的加成计算公式。

创建 EffectProcessor.ts，实现一个静态方法或单例服务 processEffects(effects: any[], source: EntityData, target: EntityData, battleManager: BattleManager)。

在 processEffects 中使用 Switch/Case 或策略模式，实现对 Damage, Block, DrawCard, ApplyBuff 这四种原子效果的具体处理。
[执行完此阶段请暂停并向我汇报]

第三阶段：全链路接入与测试验证

更新 CardManager.ts：玩家从牌库抽牌时，通过 ConfigManager 读取真实数据实例化卡牌。

重构卡牌打出逻辑：在 UI 层拖拽释放卡牌后，调用 EffectProcessor.processEffects，传入玩家数据、锁定的敌人数据和卡牌的 effects 配置。

确保打出卡牌后，UI（如血量、格挡、Buff层数图标等）能正确通过事件总线通知刷新。
[最终完成汇报]

【输出要求】

JSON 结构必须清晰且利于策划扩展。

EffectProcessor 的设计必须解耦，方便未来添加更多新效果（如：丢弃手牌、增加最大生命等）。

请通过代码生成直接写入我的工作区。
```

---

之前的框架只有基本的卡牌效果，为了规范化卡牌效果，为后续的开发能够有更高的自由度，将卡牌效果用配置表的模式进行开发。

```yaml
【当前阶段目标】

基于已有的关卡系统和战斗状态机，我现在需要对卡牌系统进行彻底的重构与升级。
目标是：实现卡牌数据驱动，通过 CardConfig.json 读取卡牌信息；并建立一套可扩展的多重效果解析系统（Effect System）与基础 Buff 系统，以支持复杂多样的卡牌行为。

【核心需求与设计规范】

1. 卡牌配置表 (CardConfig.json)

在 assets/resources/configs/ 下新增 CardConfig.json。

核心设计：每张卡牌需要支持“多重效果”。例如一张卡既能造成伤害，又能上 Buff，还能抽牌。

字段示例：id, name, cost, type (Attack/Skill/Power), target (SingleEnemy/AllEnemies/Self), description。

关键字段 effects：一个数组，定义该卡牌触发的一系列原子效果。

例如：[{"type": "Damage", "value": 6}, {"type": "ApplyBuff", "buffId": "vulnerable", "value": 2}]。

2. 原子效果处理器 (EffectProcessor)

编写 EffectProcessor.ts（或类似的管理类），负责解析和执行 JSON 中定义的 effects 数组。

需要支持的基础原子效果类型：

Damage (造成伤害)

Block (获得格挡)

DrawCard (抽牌)

Heal (回血)

ApplyBuff (施加状态)

3. 基础状态/Buff 系统 (Buff System)

扩展 EntityData（实体类），为其添加一个状态列表（如 Map<string, number> 记录 Buff 及其层数）。

实现 2 个基础 Buff 的结算逻辑（为了验证系统）：

Strength (力量)：增加攻击卡牌造成的伤害。

Vulnerable (易伤)：受到的伤害增加 50%。

4. 动态打牌逻辑重构

修改 CardManager.playCard 和 BattleManager：打出卡牌时，不再硬编码“打击/防御”的逻辑，而是将卡牌的 effects 数组交由 EffectProcessor 遍历执行，并传入正确的施法者 (Player) 和目标 (Target)。

【任务拆解与执行步骤】

请严格按照以下三个阶段分步执行，并在一阶段完成后暂停等待我的指令。

第一阶段：配置表生成与加载

创建 CardConfig.json，在其中设计 4 张具有代表性的测试卡牌：

普通攻击（单体伤害）

普通防御（单体格挡）

痛击（造成伤害 + 给予2层易伤）

肌肉记忆（0费，获得2层力量 + 抽1张牌）

更新已有的 ConfigManager.ts，增加对 CardConfig.json 的异步加载和解析逻辑，提供 getCardConfigById 方法。

更新 CardData.ts 接口，使其与 JSON 结构对齐。
[执行完此阶段请暂停并向我汇报，等待我确认 JSON 结构]

第二阶段：Buff 系统与效果解析器

修改 EntityData.ts，加入基础的 Buff 管理方法（addBuff, getBuffStack）。并在其 takeDamage 等方法中，接入“易伤”和“力量”的加成计算公式。

创建 EffectProcessor.ts，实现一个静态方法或单例服务 processEffects(effects: any[], source: EntityData, target: EntityData, battleManager: BattleManager)。

在 processEffects 中使用 Switch/Case 或策略模式，实现对 Damage, Block, DrawCard, ApplyBuff 这四种原子效果的具体处理。
[执行完此阶段请暂停并向我汇报]

第三阶段：全链路接入与测试验证

更新 CardManager.ts：玩家从牌库抽牌时，通过 ConfigManager 读取真实数据实例化卡牌。

重构卡牌打出逻辑：在 UI 层拖拽释放卡牌后，调用 EffectProcessor.processEffects，传入玩家数据、锁定的敌人数据和卡牌的 effects 配置。

确保打出卡牌后，UI（如血量、格挡、Buff层数图标等）能正确通过事件总线通知刷新。
[最终完成汇报]

【输出要求】

JSON 结构必须清晰且利于策划扩展。

EffectProcessor 的设计必须解耦，方便未来添加更多新效果（如：丢弃手牌、增加最大生命等）。

请通过代码生成直接写入我的工作区。
```
