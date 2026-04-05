<div align="center">

# simp-player-skill

> *"你知道自己在舔，但就是停不下来——或者，你知道自己在玩，但不知道什么时候开始认真了。"*

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-Skill-blueviolet)](https://claude.ai/code)
[![AgentSkills](https://img.shields.io/badge/AgentSkills-Standard-green)](https://agentskills.io)

<br>

建模的不是别人，是你自己。<br>
选一种模式——舔狗或海王——然后和不同的人对话。<br>
每一次对话都会留下痕迹，数字人会从中成长，或者退回去。<br>

**把自己的关系模式提炼成数字人，看它在不同人面前会变成什么样子。**

<br>

[核心概念](#核心概念) · [安装](#安装) · [使用](#使用) · [效果示例](#效果示例) · [**English**](README_EN.md)

</div>

---

## 核心概念

### 模式谱

数字人不是二选一的开关，而是在一条连续谱上运动：

```
-100 ←————————————————————————————→ +100
纯舔狗                              纯海王
```

- **舔狗端**：焦虑依恋、高追求强度、讨好、遇冷加倍追
- **海王端**：回避依恋、制造稀缺感、多线操控、情感掌控
- **中间段（-20 ~ +20）**：矛盾行为，是最接近真实人的区间

### 成长机制

位置由**对话中发生的真实事件**驱动，不是时间流逝自动推进：

| 触发事件 | 方向 |
|---------|------|
| 被拒绝、被忽视、被利用 | ← 更舔狗 |
| 成功撤退、识别操控、表达边界 | → 更海王 |
| 破防时刻（海王状态下情感失控） | ← 退回舔狗 |

你可以随时声明想切换到另一个方向，数字人会开始往那里靠——但不会直接切换，而是在每次对话里留下越来越明显的痕迹。

### 对手方

每次对话的另一方从你提供的聊天记录或描述中分析生成，系统会识别：
- 依恋倾向（焦虑型 / 回避型 / 安全型 / 混乱型）
- 冲突处理风格
- 爱之语（给出型 vs 渴求型）
- 自我价值感水平
- 追求节奏

不同类型的对手方会对数字人产生不同的影响——被高冷型反复晾着，和被热情型全力追求，会把数字人推向完全不同的位置。

---

## 安装

### Claude Code

```bash
# 安装到当前项目（在 git 仓库根目录执行）
mkdir -p .claude/skills
git clone https://github.com/ryanzhu95/simp-player-skill .claude/skills/simp-player

# 或安装到全局（所有项目都能用）
git clone https://github.com/ryanzhu95/simp-player-skill ~/.claude/skills/simp-player
```

---

## 使用

在 Claude Code 中输入：

```
/simp-player
```

首次运行会完成初始化：选择起始模式，可选喂入自己的聊天记录。  
之后每次运行选择对手方，开始对话，结束时自动复盘。

### 常用指令

| 说什么 | 效果 |
|--------|------|
| `切换目标模式：海王` | 数字人开始往海王方向靠拢 |
| `追加记录` | 补充对手方的聊天数据，更新画像 |
| `更新我的数据` | 补充自身数据，更新数字人人格 |
| `这不对，我不会这样说` | 纠正数字人行为，写入最高优先级修正层 |
| `结束对话` | 触发复盘，更新成长状态 |

---

## 效果示例

> 初始设置：男，28 岁，天蝎座，舔狗模式（position = -75）

**对手方：高冷型，刚发来"最近有点忙"**

*position = -75（舔狗区间）*
```
对手方          ❯ 最近有点忙

数字人（内心）  ❯ TA 在暗示什么吗？还是真的忙？不管了先表示理解。
数字人          ❯ 没事，你忙你的，有需要帮忙的话跟我说
                ❯ 那你有空了咱们出来吃个饭？我来找你就行
                ❯ （对方已读未回，五分钟后）
                ❯ 不用担心我，我这边随时都行
```

*同样的消息，position = 0（过渡区间）*
```
对手方          ❯ 最近有点忙

数字人（内心）  ❯ 要关心吗？但是……算了，先冷一下。
数字人          ❯ 嗯，忙完了再说吧
                ❯ （沉默 20 分钟后）
                ❯ 还好吗
```

*position = -60，目标 = +50（舔狗身体，海王灵魂）*
```
对手方          ❯ 最近有点忙

数字人（内心）  ❯ 想问问 TA 在忙什么——但忍住了。这次不追。
数字人          ❯ 好，等你
                ❯ （没有继续追问）
```

**对话复盘**
```
[本次对话复盘]

触发事件：
  · 被晾着未回复（← 舔狗 -10）

位置变化：-75 → -80（lower_bound 限制，实际可移动范围已到边界）
SWI 变化：32 → 29

积压张力：5（方向：← 舔狗）
原因：想进一步退回但被范围约束，这股张力会带入下次对话开场。
```

---

## 项目结构

```
simp-player-skill/
├── SKILL.md                     # skill 入口
├── lenses/                      # 人格分析视角库
│   ├── attachment.md            #   依恋模式
│   ├── conflict.md              #   冲突风格
│   ├── love_language.md         #   爱之语
│   ├── self_worth.md            #   自我价值感（SWI）
│   └── chase_rhythm.md          #   追求节奏
├── digital_human/               # 数字人状态（gitignored 用户数据）
│   ├── persona.md               #   人格（Layer 0–4）
│   ├── mode.md                  #   模式谱位置与范围参数
│   ├── growth_log.md            #   成长记录（只追加）
│   └── self_worth_tracker.md   #   SWI 变化轨迹
├── users/sessions/              # 对手方画像（gitignored 用户数据）
├── prompts/
│   ├── intake.md                #   数据喂入入口
│   ├── user_analyzer.md         #   调用 lenses，生成人格画像
│   ├── interaction.md           #   对话主逻辑
│   ├── debrief.md               #   对话复盘 + 位置更新
│   ├── merger.md                #   增量数据合并
│   └── correction_handler.md   #   纠正层写入
└── docs/
    ├── PRD.md
    └── TEST.md
```

---

<div align="center">

MIT License © [titanwings](https://github.com/titanwings)

</div>
