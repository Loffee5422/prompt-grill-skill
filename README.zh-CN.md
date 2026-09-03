# Prompt Grill：把模糊想法打磨成可直接使用的 Prompt

Prompt Grill 是一个 Agent Skill，用持续但不压迫的单问题追问，把尚未成形的想法磨成用户认可、能够直接投入使用的 prompt。它的关键区别是：先提出具体理解，再只问当前最影响质量的一个问题；每轮都更新草稿，直到用户明确要求收尾。

[English](README.md)

## 安装

技能的规范地址：

```text
https://github.com/Loffee5422/prompt-grill-skill/tree/main/skills/prompt-grill
```

可以把下面这句话直接交给兼容的智能体：

```text
从 https://github.com/Loffee5422/prompt-grill-skill/tree/main/skills/prompt-grill 安装 `prompt-grill` 技能
```

使用 Codex 自带的 GitHub 技能安装器：

```bash
python3 "${CODEX_HOME:-$HOME/.codex}/skills/.system/skill-installer/scripts/install-skill-from-github.py" \
  --url https://github.com/Loffee5422/prompt-grill-skill/tree/main/skills/prompt-grill
```

需要固定版本时，使用首个发布版本：

```text
https://github.com/Loffee5422/prompt-grill-skill/tree/v1.0.0/skills/prompt-grill
```

## 能做什么

- 从用户已经给出的信息出发，即使想法还很粗糙。
- 每轮先带着具体理解或草稿确认，不空手提问。
- 一次只问一个问题，并优先处理最影响最终质量的模糊点。
- 每轮回答后更新工作草稿，并简要说明变化。
- 面对“随便”或“你决定”等含糊回答时，提出有理由的默认方案，但不暗自决定重要事项。
- 在用户发出明确退出信号前持续打磨。
- 收尾时给出完整、干净、可直接使用的最终 prompt。

## 适用场景

- 为 Claude、ChatGPT、Codex 或其他模型打磨系统 prompt。
- 为产品功能或内部流程制作可重复调用的 prompt。
- 明确输出格式、篇幅、语气、约束、边界情况、示例与验收标准。
- 修复结果不稳定或要求不清楚的现有 prompt。

## 工作方式

智能体维护一份持续演进的草稿，每轮只选择一个最值得澄清的问题。大致优先关注使用者与场景、期望产出、约束与禁区、边界情况、具体例子和判断标准，但不会机械地走完清单。

只有用户明确表示满意、停止追问或直接给结果时，智能体才进入收尾阶段。最终输出会把必要信息自然组织成一份完整 prompt，不强塞无用模板标题，也不混入与 prompt 无关的元评论。

完整操作说明位于 [`skills/prompt-grill/SKILL.md`](skills/prompt-grill/SKILL.md)。

## 常见问题

### 会一次问很多问题吗？

不会。每轮只问一个当前最重要的问题，避免让澄清本身变成负担。

### 会固定问满多少轮吗？

不会。简单需求可以少问，复杂需求可以多问；轮数服务于对齐，而不是完成流程。

### 用户不想继续回答怎么办？

“可以了”“就这样”“别问了”“直接给我”“stop”等都属于退出信号。智能体会立即整理最终 prompt，并提醒仍未完全对齐的少数事项，而不是继续追问。

### 用户让智能体自行决定怎么办？

智能体会给出一个合理默认方案及简短理由，但重要决策仍会显式交给用户确认或修改。

## 限制

- 最终 prompt 的质量仍取决于对话中获得的信息和用户确认的决定。
- 本技能改善的是需求表达与对齐，不能保证所有下游模型或工具表现完全一致。
- 它刻意采用交互式流程，不适合明确要求完全不追问的一次性生成场景。

## 参与贡献

请参阅 [CONTRIBUTING.md](CONTRIBUTING.md)。修改应保留“一次一个问题”、草稿可见演进和用户主动退出这三个核心特征。

## 许可证

本项目采用 [MIT License](LICENSE)。
