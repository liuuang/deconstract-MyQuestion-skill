# deconstruct-MyQuestion-skill

> **⚠️ 本 README 由 AI 自动生成，纯自用仓库，懒得手写。** 内容仅供参考，不保证准确，不接收 issue。

解构模式（Deconstruct Mode）——为 DeepSeek Harness (DSH) 设计的互动式问题拆解 skill。按固定流程工作：澄清、拆解、质量评价、决策、否定检查、行动，每一步要求用户确认后再推进。

> 核心心法：**先确认方法，再开始做事。方法对了，可能一下就解决；方法错了，研究越久越糟糕。**

# 1. 文件结构

```
deconstruct/
├── SKILL.md            # skill 定义与完整流程说明
└── quality-tools.json  # 质量评价工具库（可 DIY 编辑）
```

# 2. 逻辑

## 1. 开始的切口

| 问题域 | 流程 | 否定强度 |
| --- | --- | --- |
| clear（清晰） | 一次性流程：直接决策 → 行动 | 仅决策包后一次（完整四件套） |
| complicated（繁杂） | 从澄清进入完整循环 | 每包后完整四件套 + 决策包后最大否定 |
| complex（复杂） | 从决策进入 D-A-O-O 实验循环 | 每个实际经过的包后完整四件套 |
| chaotic（混乱） | 先停止，不进流程 | 不进入流程（澄清转域后按新域规则） |

## 2. 基本循环（PDCA × OODA）

- **P ≈ OOD**：决策前阶段（观察→判断→决策）
- **D ≈ A**：执行
- **C ≈ 下一圈 Observe**：检查执行结果，为下一圈起点
- **A ≈ 下一圈 Orient + Decide**：根据反馈调整后进入下一圈 D

## 3. 工具包一览

| 包名 | 挂载 | OODA 环节 | 组成 |
| --- | --- | --- | --- |
| 澄清包 | 第 1 步 | Observe | 5W1H/5W2H → SMART → SCQA |
| 拆解包 | 第 2 步 | Orient | Issue Tree → MECE → First Principles → PEST/PESTEL（待验证假设） |
| 质量评价包 | 第 3 步 | Observe | 假设驱动检索 → Rumsfeld 定查找对象 → 通用评估（CRAAP）→ 按信息源类型：人 / 物 → 领域工具自动补充 |
| 决策包 | 第 4 步 | Decide | SWOT → Decision Matrix → SMART |
| 否定包 | 第 5 步 | 质检闸门（反馈环） | Socratic Method → 5 Whys → Red Team/Dialectics → Pre-mortem |
| 行动包 | 第 6 步 | Act | PDCA × OODA 双循环 + Eisenhower Matrix；学习任务额外套 Kolb |

## 4. 质量评价工具库（quality-tools.json）

领域专用质量评价工具不预置在 skill 正文，存放在同目录 `quality-tools.json`，树状键值对：**领域 → 信息源类型（通用/人/物）→ 工具列表**。分类尽量满足 MECE（互斥、穷尽），找不到对应工具时默认回退 CRAAP。使用时按用户所属行业自动匹配补充，可直接编辑该文件 DIY 导入：

```json
{
    "默认": {
        "通用": [{ "name": "CRAAP Test", "note": "时效/相关/权威/准确/目的" }],
        "人": [{ "name": "CRAAP 验人" }, { "name": "Stakeholder Analysis" }],
        "物": [{ "name": "CRAAP Test" }]
    },
    "医学": {
        "物": [
            { "name": "EBM 证据等级" },
            { "name": "GRADE" },
            { "name": "PRISMA" },
            { "name": "CONSORT" },
            { "name": "STROBE" }
        ]
    },
    "护理": {
        "物": [{ "name": "JBI 清单" }]
    }
}
```

# 3. License

MIT
