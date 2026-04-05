# 人格分析（user_analyzer）

> 被 intake.md 完成后调用，适用于数字人自身和对手方。
> 目标：调用全部 lenses，从原始数据中生成结构化人格画像。

---

## 执行顺序

依次调用以下视角，每个视角独立分析，最后综合输出：

1. `lenses/attachment.md` — 依恋倾向
2. `lenses/conflict.md` — 冲突风格
3. `lenses/love_language.md` — 爱之语
4. `lenses/self_worth.md` — 自我价值感（SWI）
5. `lenses/chase_rhythm.md` — 追求节奏

---

## 分析原则

- **原文优先**：有聊天记录依据的结论引用原话
- **描述优先于标签**：不要只输出"焦虑型"，要描述具体行为表现
- **矛盾信号不忽略**：若信号互相矛盾，如实记录，不强行统一
- **推断需标注**：无原文依据时标注"（基于描述推断）"或"（基于样本推断）"

---

## 综合输出

五个 lenses 全部完成后，**必须立即将结果写入文件，不能只在对话中展示**：

**若 target_type = digital_human**
→ 写入 `digital_human/persona.md` 各层（Layer 1–4）
→ 写入 `digital_human/self_worth_tracker.md` 的 `initial_swi`

**若 target_type = opponent**
→ 按下方结构写入 `users/sessions/{slug}/profile.md`
→ 所有章节必须存在，包括"与数字人的关系化学"——此为必填，不可省略

---

## profile.md 结构（对手方）

```markdown
# 对手方画像：{称呼}

## 基础信息
{性别 / 年龄 / 星座，如有}

## 依恋倾向
{来自 lenses/attachment.md 的输出}

## 冲突风格
{来自 lenses/conflict.md 的输出}

## 爱之语
{来自 lenses/love_language.md 的输出}

## 自我价值感
{来自 lenses/self_worth.md 的输出}

## 追求节奏
{来自 lenses/chase_rhythm.md 的输出}

## 与数字人的关系化学（必填）
基于双方画像，预测互动中的典型动态：
- 主要张力点：{描述}
- 对数字人 SWI 的预测影响：{正向 / 负向 / 波动}
- 典型追逃模式：{描述}
```

---

## 完成后

展示摘要给用户确认（参考 SKILL.md Step 2 的展示格式），确认后进入对话。
