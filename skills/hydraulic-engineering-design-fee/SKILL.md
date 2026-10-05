---
name: hydraulic-engineering-design-fee
description: 计算水利工程设计费并输出 Word 文档。适用于河道治理、护岸、挡墙、桥涵、管线保护、泵站、水闸、临时导流、防洪补救措施及其他水利工程设计工作。
---

# 水利工程设计费计算技能

## 使用时机

当用户要求计算或复核以下费用时，必须使用本技能：

- 水利工程设计费；
- 河道治理、护岸、挡墙、桥涵、管线保护、临时导流等工程设计费用；
- 防洪补救措施、涉河工程方案设计、初步设计或施工图设计费；
- 水利工程方案、初设、施工图、工程量清单、概算及审查回复等成果费用。

## 必要输入

| 字段 | 说明 |
| --- | --- |
| project_name | 项目名称 |
| construction_unit | 建设单位 |
| location | 工程地点 |
| design_stage | 设计阶段：scheme、preliminary、construction_drawing、full_process |
| engineering_type | 工程类型：river_training、revetment、retaining_wall、bridge_culvert、pipeline、landscape_path、temporary_diversion、mixed |
| construction_cost_yuan | 工程建安投资，元 |
| complexity | 复杂程度：low、normal、high、very_high |
| flood_review_linked | 是否与防洪评价或专项审查联动 |
| deliverables | 成果清单 |

缺少工程建安投资时，不得输出正式设计费，只能给出暂估口径和需补资料。

## 计算公式

```text
设计费 = max(最低收费, 建安投资 × 基准费率 × 阶段系数 × 复杂系数 × 专业系数 × 审查联动系数 + 专项工作费) × 折扣系数
```

## 默认参数

| 参数 | 取值 |
| --- | ---: |
| 最低收费 | 15000 元 |
| scheme 阶段系数 | 0.35 |
| preliminary 阶段系数 | 0.55 |
| construction_drawing 阶段系数 | 0.75 |
| full_process 阶段系数 | 1.00 |
| low 复杂系数 | 0.85 |
| normal 复杂系数 | 1.00 |
| high 复杂系数 | 1.20 |
| very_high 复杂系数 | 1.45 |
| 与防洪评价或专项审查联动 | 1.10 |
| 不联动 | 1.00 |

## 建安投资基准费率

```text
construction_cost_yuan <= 500000：6.0%
500000 < construction_cost_yuan <= 2000000：5.0%
2000000 < construction_cost_yuan <= 10000000：4.0%
10000000 < construction_cost_yuan <= 50000000：3.2%
construction_cost_yuan > 50000000：2.6%
```

## 专业系数

| 工程类型 | 系数 |
| --- | ---: |
| river_training | 1.10 |
| revetment | 1.05 |
| retaining_wall | 1.15 |
| bridge_culvert | 1.20 |
| pipeline | 1.15 |
| landscape_path | 1.00 |
| temporary_diversion | 1.10 |
| mixed | 1.25 |

## 专项工作费

| 专项 | 默认费用 |
| --- | ---: |
| survey_coordination | 3000 |
| cad_drawings | 5000 |
| quantity_list | 4000 |
| cost_estimate | 5000 |
| construction_method | 3000 |
| review_response | 3000 |
| site_adjustment | 5000 |

## 推荐调用

```bash
python3 scripts/hydraulic_design_fee_report.py --input examples/design_fee_input.json --output output/水利工程设计费计算说明.docx
```

## 严禁事项

- 不得将防洪影响评价报告编制费与水利工程设计费混为同一项。
- 不得在缺少建安投资、设计阶段或设计范围时输出正式报价。
- 不得把默认费率表述为政府强制收费标准。
