# 水利咨询费用计算技能包

## Muse 入口

如果 Muse 没有自动识别 `.codex/skills`，请让它优先读取：

```text
MUSE.md
skills/hydraulic-engineering-design-fee/SKILL.md
skills/flood-impact-compilation-fee/SKILL.md
```

仓库地址：

```text
https://github.com/lish964121/hydro-fee-calculation-skills
```

本仓库包含两个可供 Codex、Muse、Claude Code 等智能体调用的技能：

1. `flood-impact-compilation-fee`：防洪影响评价报告编制费计算。
2. `hydraulic-engineering-design-fee`：水利工程设计费计算。

两个技能均可读取 JSON 参数，输出 Word 计算说明书，适用于报价测算、内部复核和与业主沟通。

## 目录结构

```text
MUSE.md
skills/flood-impact-compilation-fee/SKILL.md
skills/hydraulic-engineering-design-fee/SKILL.md
.codex/skills/flood-impact-compilation-fee/SKILL.md
.codex/skills/hydraulic-engineering-design-fee/SKILL.md
examples/compilation_fee_input.json
examples/design_fee_input.json
scripts/flood_compilation_fee_report.py
scripts/hydraulic_design_fee_report.py
docs/agent_usage.md
```

## 安装依赖

```bash
pip install -r requirements.txt
```

## 生成防洪影响评价编制费 Word

```bash
python3 scripts/flood_compilation_fee_report.py \
  --input examples/compilation_fee_input.json \
  --output output/防洪影响评价编制费计算说明.docx
```

## 生成水利工程设计费 Word

```bash
python3 scripts/hydraulic_design_fee_report.py \
  --input examples/design_fee_input.json \
  --output output/水利工程设计费计算说明.docx
```

## 使用原则

- 本仓库默认规则属于工程咨询报价测算口径，不是政府强制收费标准。
- 项目已有合同、公司报价标准或地方主管部门固定口径时，应优先采用固定口径。
- 缺少关键资料时，只能输出暂估测算，并在 Word 中列出需核实项。
- 正式报价前，应由项目负责人或总工复核项目范围、成果清单、评审深度和后续服务内容。
