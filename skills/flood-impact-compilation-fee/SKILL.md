---
name: flood-impact-compilation-fee
description: 计算防洪影响评价报告编制费、咨询费和报价说明，并输出 Word 文档。适用于河道管理范围内建设项目、防洪评价报告、桥梁、管线、慢道、公园、岸线整治及涉河建筑物等项目。
---

# 防洪影响评价报告编制费计算技能

## 使用时机

当用户要求计算或复核以下费用时，必须使用本技能：

- 防洪影响评价报告编制费；
- 防洪评价咨询费；
- 防洪影响评价报价说明；
- 涉河建设项目评价报告、评审配合、模型计算和附图成果费用。

## 必要输入

| 字段 | 说明 |
| --- | --- |
| project_name | 项目名称 |
| construction_unit | 建设单位 |
| location | 工程地点 |
| project_type | 工程类型 |
| river_level | 河道管理等级：一般河道、区管、市管、省管、山洪沟 |
| river_length_km | 涉河或评价河段长度，km |
| area_ha | 评价范围面积，hm2 |
| hydraulic_model | 水力模型深度：none、simple、one_d、two_d |
| complexity | 复杂程度：low、normal、high、very_high |
| review_level | 评审深度：none、normal、multiple_rounds、expert_meeting |
| deliverables | 成果清单 |

资料不全时，可以暂估，但不得输出确定性正式报价，必须列出需核实项。

## 计算公式

```text
编制费 = max(最低收费, 基础编制费 × 规模系数 × 复杂系数 × 河道系数 × 模型系数 × 评审系数 + 专项工作费) × 折扣系数
```

## 默认参数

| 参数 | 取值 |
| --- | ---: |
| 基础编制费 | 30000 元 |
| 最低收费 | 25000 元 |
| low 复杂系数 | 0.85 |
| normal 复杂系数 | 1.00 |
| high 复杂系数 | 1.25 |
| very_high 复杂系数 | 1.50 |
| 一般河道系数 | 0.90 |
| 区管河道系数 | 1.00 |
| 市管河道系数 | 1.15 |
| 省管河道系数 | 1.30 |
| 山洪沟系数 | 1.05 |
| none 模型系数 | 0.85 |
| simple 模型系数 | 1.00 |
| one_d 模型系数 | 1.20 |
| two_d 模型系数 | 1.45 |
| none 评审系数 | 0.95 |
| normal 评审系数 | 1.00 |
| multiple_rounds 评审系数 | 1.15 |
| expert_meeting 评审系数 | 1.25 |

## 推荐调用

```bash
python3 scripts/flood_compilation_fee_report.py --input examples/compilation_fee_input.json --output output/防洪影响评价编制费计算说明.docx
```

## 严禁事项

- 不得把本技能默认参数写成政府强制收费标准。
- 不得在缺少项目规模、河道等级和模型深度时输出正式报价。
- 不得遗漏二维模型、专家会、多轮补充、GIS 制图、PPT 汇报等实际工作量。
