# deconstruct-MyQuestion-skill

解构模式（Deconstruct Mode）——一个为 DeepSeek Harness (DSH) 设计的互动式问题拆解 skill。像 /plan 一样工作，但更彻底：把一次完整的问题解决过程组织为一次 OODA 循环，从澄清、拆解、取证、决策到执行前红队审查，每一步都要求用户确认后再推进。

> 核心心法：**先确认方法，再开始做事。方法对了，可能一下就解决；方法错了，研究越久越糟糕。**

## 特性

- **固定流程**：不是自由聊天，每步一个标准提问，等用户回答后进入下一步
- **OODA 架构**：观察 → 判断 → 决策 → 执行，外加循环前的定位与执行前的质检闸门
- **工具按包组织**：工具不零散调用，按"包"挂载到对应步骤，包内分工顺序固定
- **否定检查**：决策执行前强制红队审查（Socratic → 5 Whys → Red Team → Pre-mortem）
- **用户控制**：支持 `继续` / `跳步` / `全部` / `停止` / `深入` 指令

## 安装

将 `deconstruct` 目录放入 DSH 的 skills 目录：

```bash
# 本仓库克隆后
cp -r deconstruct ~/.dsh/skills/
```

确认 skill 已被识别（会话中应出现 deconstruct skill 条目）。

## 用法

```
/deconstruct <你的问题>
```

例如：

```
/deconstruct 我想了解医学新闻
/deconstruct 要不要换工作
/deconstruct 毕业论文选题怎么定
```

## 流程架构

整个流程 = 一次 OODA 循环 + 循环前"定位" + 执行前"质检闸门"：

```
定位（循环前）  第 0 步 元检查 —— Cynefin 定问题域 + Rumsfeld 盘知识状态，选方向
Observe 观察    第 1 步 澄清    —— 收集问题现状
Orient 判断     第 2 步 拆解    —— 拆结构、列假设、出候选方案
Decide 决策     第 3 步 获取信息 —— 为候选方案收集证据
               第 4 步 决策    —— SWOT → Decision Matrix → SMART
质检闸门        第 5 步 否定检查 —— 决策执行前的红队审查
Act 执行        第 6 步 行动    —— PDCA + Eisenhower 落地
```

## 工具包一览

| 包名 | 挂载 | 组成 |
| --- | --- | --- |
| 澄清包 | 第 1 步 | 5W1H/5W2H → SMART → SCQA |
| 拆解包 | 第 2 步 | Issue Tree → MECE → First Principles → PEST/PESTEL |
| 获取信息包 | 第 3 步 | CRAAP 信源评估 → 静态 DLC：PICO / 人际 DLC：Stakeholder → Power-Interest Grid |
| 决策包 | 第 4 步 | SWOT → Decision Matrix → SMART |
| 否定包 | 第 5 步 | Socratic Method → 5 Whys → Red Team/Dialectics → Pre-mortem |
| 行动包 | 第 6 步 | PDCA + Eisenhower Matrix；学习任务额外套 Kolb |

## 用户控制指令

- **直接回答**：可以选 A/B/C，也可以自由输入
- `继续`：当前步骤用合理默认值推进
- `跳步`：跳过当前步骤
- `全部`：不再交互，一次性输出完整解构
- `停止`：结束本次解构
- `深入`：对当前步骤递归否定检查

## 文件结构

```
deconstruct/
└── SKILL.md     # skill 定义与完整流程说明
```

## License

MIT
