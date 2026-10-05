# 智能体调用说明

## 技能选择

| 用户任务 | 应调用技能 |
| --- | --- |
| 算防洪影响评价报告、咨询、评审配合、模型分析费用 | flood-impact-compilation-fee |
| 算水利工程设计费，如河道治理、护岸、挡墙、桥涵、管线、导流、补救措施等设计费用 | hydraulic-engineering-design-fee |

## 防洪影响评价编制费调用指令

```text
请使用 .codex/skills/flood-impact-compilation-fee/SKILL.md 的规则，
根据项目资料计算防洪影响评价报告编制费，并调用
scripts/flood_compilation_fee_report.py 输出 Word 文档。
资料缺失时只输出暂估测算，并列出需核实项。
```

## 水利工程设计费调用指令

```text
请使用 .codex/skills/hydraulic-engineering-design-fee/SKILL.md 的规则，
根据建安投资、设计阶段、工程类型和成果范围计算水利工程设计费，
并调用 scripts/hydraulic_design_fee_report.py 输出 Word 文档。
资料缺失时只输出暂估测算，并列出需核实项。
```

## 运行命令

```bash
python3 scripts/flood_compilation_fee_report.py --input examples/compilation_fee_input.json --output output/防洪影响评价编制费计算说明.docx
python3 scripts/hydraulic_design_fee_report.py --input examples/design_fee_input.json --output output/水利工程设计费计算说明.docx
```

## 复核要点

1. 防洪影响评价报告编制费和水利工程设计费应分开列项，不应重复计取同一工作内容。
2. 编制费重点复核河道等级、评价范围、模型深度、评审轮次和成果清单。
3. 设计费重点复核建安投资、设计阶段、专业复杂度、是否含概算或工程量清单。
4. 形成正式报价前，应由项目负责人或总工复核。
