# Browser Pro Research Orchestrator

[English](README.md) · **简体中文** · [Français](README.fr.md)

把已登录的浏览器会话与仅网页端可用的 Pro 模型组织成一组缓慢但彼此独立的研究专家，同时让 Codex 继续负责整体编排、批判性审查和最终决策。

![Browser Pro Research Orchestrator 科研流程图](docs/browser-pro-research-orchestrator.jpg)

## 为什么需要这个 Skill

复杂项目往往不是因为缺少某一个想法而失败，而是因为多个困难模块需要独立调研；它们的假设、接口与职责必须一致；最终方案还必须满足数据规模、算力、工程接口和部署条件。

网页端 Pro 模型通常能提供更广、更深入的分析，但单个超长对话并不等于有组织的研究。它容易混合不同模块、遗失硬约束，或过早接受自己提出的复杂方案。

这个 Codex Skill 提供了缺失的研究编排层。

## 它能做什么

- 将复杂项目拆分为 2–5 个边界明确的研究模块；
- 通过用户现有的 Chrome 登录会话，为不同模块建立独立的 Pro 对话；
- 每次发送前核对项目、模型和推理模式；
- 编写上下文充分的提示词，要求普通网页检索与一手文献证据；
- 等待较慢的长回答，绝不点击 **Answer now** 或提前终止；
- 从证据质量、数据泄漏、可行性、复杂度和运行成本等方面审查方案；
- 发送聚焦的修订提示，或在对话走偏时重新开新线程；
- 审计模块之间的接口、术语和职责边界；
- 综合为可实现、可证伪且带有 go/no-go 条件与回退方案的设计。

该流程不限定领域，可用于软件架构、计算机视觉、机器学习、科研 pipeline、系统工程、产品设计等多模块研究任务。

## 工作流程

```text
DISCOVER
→ CONTEXT_LOCK
→ DECOMPOSE
→ MODEL_VERIFY
→ PROMPTS_READY
→ THREADS_SENT
→ WAITING
→ REVIEW
→ REVISE
→ CROSS_AUDIT
→ SYNTHESIZE
→ COMPLETE
```

Pro 模型在这里是“研究方案提出者”，而不是权威。只有当证据、假设、计算预算、评估协议、失败模式和跨模块接口都可审查时，一个模块才会被接受。

## 安装

首先克隆本仓库：

```bash
git clone <repository-url>
cd browser-pro-research-orchestrator
```

### Codex 与 Kimi Code

Codex 和 Kimi Code 都会扫描共享的用户级 Agent Skills 目录，因此只需安装一次：

```bash
mkdir -p ~/.agents/skills
cp -R skill/browser-pro-research-orchestrator ~/.agents/skills/
```

如果只希望在单个项目中使用，请复制到：

```text
<项目根目录>/.agents/skills/browser-pro-research-orchestrator/
```

如果新创建的顶层 Skills 目录没有立即被识别，请重启对应的 coding agent。

### Claude Code

Claude Code 使用自己的个人 Skills 目录：

```bash
mkdir -p ~/.claude/skills
cp -R skill/browser-pro-research-orchestrator ~/.claude/skills/
```

如果只希望在单个项目中使用，请复制到：

```text
<项目根目录>/.claude/skills/browser-pro-research-orchestrator/
```

在 macOS 或 Linux 上，也可以先安装到 `~/.agents/skills/`，再为 Claude Code 建立符号链接，从而避免维护两份副本：

```bash
mkdir -p ~/.claude/skills
ln -s ~/.agents/skills/browser-pro-research-orchestrator \
  ~/.claude/skills/browser-pro-research-orchestrator
```

核心的 `SKILL.md` 工作流和 `references/` 可在三个 agent 之间通用。`agents/openai.yaml` 仅提供 Codex 界面元数据，Kimi Code 和 Claude Code 可以忽略它。

## 使用条件

- Codex、Kimi Code 或 Claude Code 已配置 Chrome 控制能力，或者配置了能够操作现有登录会话的等价浏览器连接器；
- 浏览器已登录，并且用户本身有权使用指定网页模型；
- 用户已授权创建对话与发送提示词；
- 目标项目或 workspace、模型及推理模式都已明确。

安装 Skill 只会安装研究工作流，不会自动安装浏览器连接器，也不提供订阅、账号凭据、浏览器登录状态或模型访问权限。如果宿主 agent 无法控制所需的登录浏览器或核验指定模型，本 Skill 会停止并明确报告阻塞原因。

## 使用方式

不同宿主的显式调用方式如下：

| 宿主 | 调用命令 |
| --- | --- |
| Codex | `$browser-pro-research-orchestrator` |
| Kimi Code | `/skill:browser-pro-research-orchestrator` |
| Claude Code | `/browser-pro-research-orchestrator` |

Codex 示例：

```text
使用 $browser-pro-research-orchestrator 拆分这个复杂项目，
通过 Chrome 运行多个相互独立的 Pro 调研对话，
对方案进行批判性审查，并综合出可行的实现计划。
```

Kimi Code 示例：

```text
/skill:browser-pro-research-orchestrator 请拆分这个复杂项目，
运行多个相互独立的 Pro 调研对话，批判性审查每个设计，
并综合出可实现的方案。
```

Claude Code 示例：

```text
/browser-pro-research-orchestrator 请拆分这个复杂项目，
运行多个相互独立的 Pro 调研对话，批判性审查每个设计，
并综合出可实现的方案。
```

当请求与 Skill 描述高度匹配时，agent 也可能自动调用它；但对于耗时且成本较高的长流程调研，建议显式调用。

建议提供：

- 项目目标以及调研需要支持的关键决策；
- 当前实现和真实测得的结果；
- 需要分别调研的复杂模块；
- 数据、算力、延迟和部署方面的硬约束；
- 本地文件、代码仓库、论文或已有对话；
- 指定的网页模型及推理模式；
- 禁止使用的方法，例如明确不使用 Deep Research。

在第一次进行浏览器写入前，请明确目标网页项目或 workspace 和指定模型，并授权 agent 在已说明的研究范围内创建对话、发送首轮提示词及执行后续迭代。

平台文档：[Codex Agent Skills](https://learn.chatgpt.com/docs/build-skills)、[Kimi Code Agent Skills](https://www.kimi.com/code/docs/en/kimi-code-cli/customization/skills.html)和 [Claude Code Skills](https://code.claude.com/docs/en/skills)。

## 调研与审查原则

### 证据优先于新颖性

提示词要求查找一手来源，并区分直接证据、可迁移证据和仅概念相关的证据。没有证据支持的部分必须明确标注。

### 可行性优先于复杂度

每个方案都会检查数据泄漏、推理时不存在的输入、过多的阈值或损失函数、未限定的任务数量、隐藏的人工步骤，以及是否遗漏失败病例。

### 接口优先于综合

最终跨模块审计会核对实体标识、单位、张量形状、缺失值语义、阈值所有权、校准、重试与拒识逻辑、产物来源，以及训练和推理字段的差异。

### 先修订，再接受

存在硬伤的方案会收到聚焦的勘误要求，包括具体反例，以及需要补充的公式、伪代码、接口或预算。如果一个线程积累了相互矛盾的假设，则重新建立独立对话。

## 安全与隐私

- 可复用 Skill 中不包含账号凭据、Cookie、账户 ID、固定项目 URL、对话 ID 或用户专属文件路径。
- 它只使用用户自己的登录会话，不绕过订阅、访问控制或使用额度。
- 创建对话或发送消息前必须获得授权。
- 无法使用指定模型时，不会静默替换为其他模型。
- 除非用户明确要求，否则不会启用 Deep Research。
- 单次任务的运行产物可能包含用户提供的项目链接；这些产物应保存在可复用 Skill 之外，并在分享前单独检查。

## 局限

- 网页界面和模型名称会变化，页面定位与模型核验步骤可能需要维护。
- Pro 回答可能需要数十分钟，应在不干预生成的前提下持续检查。
- 浏览器连接、登录状态、额度和模型可用性仍是外部依赖。
- 最终产物是研究设计，并不等于已经证明性能提升；仍需实现与实验验证。

## 仓库结构

```text
.
├── README.md
├── README.zh-CN.md
├── README.fr.md
├── docs/
│   └── browser-pro-research-orchestrator.jpg
└── skill/
    └── browser-pro-research-orchestrator/
        ├── SKILL.md
        ├── agents/
        │   └── openai.yaml
        └── references/
            ├── prompt-patterns.md
            └── review-rubric.md
```

## 声明

这是一个独立、非官方的 Codex Skill，与 OpenAI、ChatGPT、Google Chrome 或任何模型提供方均无隶属或背书关系。文中产品名称仅用于说明兼容性。
