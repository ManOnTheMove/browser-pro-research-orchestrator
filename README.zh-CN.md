# Browser Pro Research Orchestrator

[English](README.md) · **简体中文** · [Français](README.fr.md)

通过浏览器中的 ChatGPT GPT-6 Astra Pro，探索研究方向、构思创新点、设计课题与科研 pipeline；由本地 GPT-6 Astra Ultra 负责深入分析、批判性审查和最终建议。

![带有卡皮巴拉研究员的 Browser Pro Research Orchestrator 科研流程图](docs/browser-pro-research-orchestrator-capybara.jpg)

## 为什么需要这个 Skill

课题在尚无代码、数据集或既定方法时，也可能需要深度思考。这个 Skill 围绕当前需要做出的研究决策组织独立的浏览器分析，再由本地模型核对证据、假设、可行性和结论。

## 模型默认值

- 网页端：**GPT-6 Astra，选中 Pro 模式**，简称 GPT-6 Pro。每次发送前都核验实际模型和模式；账户上的 Pro 订阅标识不能代替模型核验。
- 本地编排模型：按 **GPT-6 Astra、Ultra 推理**的运行前提设计。Skill 不修改本地设置，也不把 Ultra 等同于网页模式或 API 参数。
- 后续任务中用户明确指定的模型优先；否则不会自动退回 GPT-5.6 Pro、Thinking、Auto 或其他模型。

这些是工作流默认值，不保证账号具备相应模型权限，也不假定网页菜单的固定文字。其他宿主 agent 仍需满足下述浏览器操作和核验条件。

## 研究模式

| 模式 | 支持的决策与产物 |
| --- | --- |
| 方向选择 | 比较科学问题，给出排序、推荐方向和下一项决定性调查。 |
| 创新点 | 构思候选贡献，对照最接近的已有工作并设计反证检验。 |
| 课题设计 | 明确研究目标、假设、协议、分析、可行性及推进／转向／停止条件。 |
| Pipeline | 制定最小基线、方法、接口、评估与实现阶段。 |
| 方案质疑 | 检查已有方向或设计的最强反对意见和替代解释。 |

按当前研究决策选择模式，必要时组合使用。支持实证、计算、理论与定性研究；早期选题不要求已有代码、数据、张量或损失函数。与课题无关的头脑风暴和常规实现工作不属于此 Skill 的范围。

## 工作流程

```text
明确当前决策，并先做本地初步分析
→ 锁定事实、假设、约束与未知信息
→ 准备最少且有用的独立研究分工
→ 核验 GPT-6 Astra + Pro，发送审阅后的提示词
→ 等待并完整读取回答
→ 核验一手证据、质疑核心主张，按需修订
→ 统一假设、结论与适用的技术接口
→ 综合研究决策及其下一项检验
```

单一问题可能只需要一个对话；困难的开放决策通常可用两到四个。后续修订聚焦具体问题，并设置预算。独立对话可以减少相互诱导，但多个模型意见一致不等于获得了独立科学证据。

流程保留长回答，不点击 **Answer now**；记录发送状态以防恢复时重复发送；模型来源无效的回答会被排除，必要咨询须在正确模型上补做。默认使用普通网页检索，只有明确要求时才启用 Deep Research。

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
- 聊天或项目目标明确，且模型与模式可以核验；不强制要求专用网页项目。

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
使用 $browser-pro-research-orchestrator，通过 Chrome 中的 GPT-6 Astra Pro
比较这个问题的研究方向，将候选创新点与最接近的已有工作对照，
并推荐可行的课题设计和第一项决定性检验。
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
- 研究阶段、可用资源，以及已有实现或真实测得的结果（如有）；
- 需要独立分析的未知问题或复杂模块；
- 数据及访问权限、时间、算力和其他相关研究约束；
- 本地文件、代码仓库、论文或已有对话；
- 如需覆盖默认 GPT-6 Astra Pro，明确指定网页模型和模式；
- 禁止使用的方法，例如明确不使用 Deep Research。

明确要求使用此 Skill 执行研究任务，即授权在该范围内创建普通研究对话和进行聚焦追问，无需逐次重复批准；目标位置须无歧义。仅修改 Skill 或准备提示词不会启动网页研究。敏感数据、上传、分享和定期监控仍遵循各自的授权要求。

平台文档：[Codex Agent Skills](https://learn.chatgpt.com/docs/build-skills)、[Kimi Code Agent Skills](https://www.kimi.com/code/docs/en/kimi-code-cli/customization/skills.html)和 [Claude Code Skills](https://code.claude.com/docs/en/skills)。

## 调研与审查原则

- **证据与新颖性：** 检查决定性一手来源和最接近的已有工作，区分直接证据、迁移假设、概念启发和未证实主张。没有检索到不等于从未有人研究。
- **可区分与可证伪：** 将主要想法与最强替代解释及可信的简单基线比较，确定最便宜且有信息价值的检验，以及推翻建议的条件。
- **符合研究阶段的可行性：** 核对资源访问、时间和科学有效性；仅在适用时检查数据泄漏、推理输入、校准、张量和计算任务预算。
- **一致性与批判：** 统一问题、文献空白、候选贡献、可获得证据与可支持结论，保留实质分歧，不以模型投票决定科学结论。
- **有边界的迭代：** 用具体反例提出窄范围修正；有依据时接受决策、暂缓有条件的主张或拒绝候选方案。复杂度和模型自评分不是证据。

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
- 最终产物支持研究决策；新颖性和有效性仍须由相应的来源核验、证明或实验确立。

## 仓库结构

```text
.
├── README.md
├── README.zh-CN.md
├── README.fr.md
├── docs/
│   └── browser-pro-research-orchestrator-capybara.jpg
└── skill/
    └── browser-pro-research-orchestrator/
        ├── SKILL.md
        ├── agents/
        │   └── openai.yaml
        └── references/
            ├── browser-protocol.md
            ├── prompt-patterns.md
            ├── research-modes.md
            └── review-rubric.md
```

## 声明

这是一个独立、非官方的 Codex Skill，与 OpenAI、ChatGPT、Google Chrome 或任何模型提供方均无隶属或背书关系。文中产品名称仅用于说明兼容性。
