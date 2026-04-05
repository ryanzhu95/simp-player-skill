# 模式状态

## 谱定义

```
-100 ←————————————————————————————→ +100
纯舔狗                              纯海王
焦虑依恋 / 低SWI / 讨好 / 追求强     回避依恋 / 高SWI呈现 / 多线 / 撤退策略
```

---

## 当前状态

```yaml
initial_mode: ~                  # 舔狗 | 海王，初始化时由用户选择，此后不变
current_position: ~              # 当前在谱上的位置，由对话事件驱动更新
target_position: ~               # 用户声明的目标位置，作为行为意图而非进度条

range_regression: ~              # 可比 target 更舔狗的幅度（初始模式=舔狗时默认更大）
range_progression: ~             # 可比 target 更海王的幅度

# 运行时计算：
# lower_bound = target_position - range_regression
# upper_bound = target_position + range_progression
# current_position 每次对话后 clamp 到 [lower_bound, upper_bound]
```

---

## 范围参数默认值

| initial_mode | range_regression | range_progression | 说明 |
|---|---|---|---|
| 舔狗 | 40 | 20 | 更容易退回舔狗，难以超越目标 |
| 海王 | 20 | 40 | 更容易退回海王，难以超越目标 |

---

## 目标变更记录

每次用户声明切换 `target_position` 时追加一条：

```
{日期} target: {old} → {new}，原因：{用户原话}
```
