# Muse 调用入口

本仓库提供两个水利费用计算技能，供 Muse、Codex、Claude Code 等智能体调用。

## 推荐优先读取

1. 水利工程设计费计算技能
   - 技能文件：`skills/hydraulic-engineering-design-fee/SKILL.md`
   - 脚本：`scripts/hydraulic_design_fee_report.py`
   - 示例：`examples/design_fee_input.json`

2. 防洪影响评价报告编制费计算技能
   - 技能文件：`skills/flood-impact-compilation-fee/SKILL.md`
   - 脚本：`scripts/flood_compilation_fee_report.py`
   - 示例：`examples/compilation_fee_input.json`

## 给 Muse 的指令示例

```text
请读取这个 GitHub 仓库：
https://github.com/lish964121/hydro-fee-calculation-skills

我要使用水利工程设计费计算技能，请优先读取：
skills/hydraulic-engineering-design-fee/SKILL.md

根据项目资料计算水利工程设计费，并调用：
scripts/hydraulic_design_fee_report.py
输出 Word 计算说明书。
```

## 注意

- `.codex/skills/` 是 Codex 标准技能目录。
- `skills/` 是给 Muse 等不一定扫描隐藏目录的智能体准备的可见镜像目录。
- 缺少关键资料时，只能输出暂估测算，并列出需核实项。
