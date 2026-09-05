# Browser Pro Research Orchestrator

**English** · [简体中文](README.zh-CN.md) · [Français](README.fr.md)

Use browser-based ChatGPT GPT-6 Astra Pro to investigate research directions, develop novel ideas, design studies, and build research pipelines, with a local GPT-6 Astra Ultra orchestrator responsible for analysis, critique, and the final recommendation.

![Browser Pro Research Orchestrator research pipeline with capybara researchers](docs/browser-pro-research-orchestrator-capybara.jpg)

## Why this skill exists

A research project can need deep reasoning before there is code, a dataset, or a chosen method. This skill coordinates independent browser analyses around the decision that matters now, then checks their evidence, assumptions, feasibility, and implications locally.

## Model defaults

- Browser: **GPT-6 Astra with Pro selected**, referred to as GPT-6 Pro. The actual model and mode must be verified in the live controls before every send; an account's Pro badge is insufficient.
- Local orchestrator: **GPT-6 Astra with Ultra reasoning**, as an operating assumption. The skill does not change local settings or equate Ultra with a web mode or API parameter.
- An explicit model choice for a later run overrides the default. Otherwise the skill never silently falls back to GPT-5.6 Pro, Thinking, Auto, or another model.

These are workflow defaults, not guarantees of model access or literal UI labels. Other host agents must still satisfy the browser and verification requirements below.

## Research modes

| Mode | Decision and deliverable |
| --- | --- |
| Direction | Choose among research questions; produce a ranked shortlist and decisive next investigation. |
| Innovation | Develop candidate contributions; compare closest prior art and define falsification tests. |
| Study | Define aims, hypotheses, protocol, analysis, feasibility, and advance/pivot/stop criteria. |
| Pipeline | Specify a minimal baseline, method, interfaces, evaluation, and implementation stages. |
| Challenge | Assess a proposed direction or design through its strongest objections and alternatives. |

Select the mode or combination that fits the current research decision. The workflow supports empirical, computational, theoretical, and qualitative research; early topic exploration does not require tensors, losses, code, or acquired data. Unrelated brainstorming and routine implementation are outside its scope.

## How it works

```text
Frame the decision and write a local provisional analysis
→ lock facts, assumptions, constraints, and unknowns
→ prepare the smallest useful set of independent workstreams
→ verify GPT-6 Astra + Pro and send reviewed prompts
→ wait and capture complete answers
→ verify primary evidence, challenge claims, and revise as needed
→ reconcile assumptions, claims, and applicable interfaces
→ synthesize a research decision and its next test
```

A narrow question may need one conversation; difficult open decisions often benefit from two to four. Follow-ups are focused and budgeted. Separate conversations reduce anchoring, but agreement between models is not independent scientific evidence.

The orchestrator preserves long responses without clicking **Answer now**, records submissions to prevent duplicates on resume, and excludes any exchange with invalid model provenance until the necessary consultation is replaced. Ordinary web search is the default; Deep Research requires an explicit request.

## Installation

Clone this repository first:

```bash
git clone <repository-url>
cd browser-pro-research-orchestrator
```

### Codex and Kimi Code

Codex and Kimi Code both scan the shared user-level Agent Skills directory, so one installation can serve both:

```bash
mkdir -p ~/.agents/skills
cp -R skill/browser-pro-research-orchestrator ~/.agents/skills/
```

For a project-only installation, copy the skill to:

```text
<project-root>/.agents/skills/browser-pro-research-orchestrator/
```

Restart the coding agent if the newly created top-level skills directory is not detected immediately.

### Claude Code

Claude Code uses its own personal skills directory:

```bash
mkdir -p ~/.claude/skills
cp -R skill/browser-pro-research-orchestrator ~/.claude/skills/
```

For a project-only installation, use:

```text
<project-root>/.claude/skills/browser-pro-research-orchestrator/
```

On macOS or Linux, you can avoid maintaining two copies by installing in `~/.agents/skills/` and linking it into Claude Code:

```bash
mkdir -p ~/.claude/skills
ln -s ~/.agents/skills/browser-pro-research-orchestrator \
  ~/.claude/skills/browser-pro-research-orchestrator
```

The `SKILL.md` workflow and its `references/` are portable across all three agents. `agents/openai.yaml` provides Codex-specific UI metadata and can be ignored by Kimi Code and Claude Code.

## Requirements

- Codex, Kimi Code, or Claude Code with a Chrome-control integration or equivalent browser connector capable of operating an existing signed-in browser session;
- an existing signed-in browser session with access to the requested web model;
- user authorization to create conversations and send prompts;
- an unambiguous chat or project destination and a verifiable target model/mode; a dedicated web project is optional.

Installing the skill installs the research workflow only. It does not install a browser connector, provide a subscription, credentials, browser login, or model access. If the host agent cannot control the required signed-in browser or verify the requested model, the skill is designed to stop and report that blocker.

## Usage

Invocation syntax differs by host:

| Host | Explicit invocation |
| --- | --- |
| Codex | `$browser-pro-research-orchestrator` |
| Kimi Code | `/skill:browser-pro-research-orchestrator` |
| Claude Code | `/browser-pro-research-orchestrator` |

Example for Codex:

```text
Use $browser-pro-research-orchestrator with GPT-6 Astra Pro in Chrome to
compare research directions for this problem, examine candidate innovations
against closest prior work, and recommend a feasible study and its first test.
```

Equivalent Kimi Code invocation:

```text
/skill:browser-pro-research-orchestrator Decompose this complex project,
run independent Pro research chats, critically review each design,
and synthesize an implementable plan.
```

Equivalent Claude Code invocation:

```text
/browser-pro-research-orchestrator Decompose this complex project,
run independent Pro research chats, critically review each design,
and synthesize an implementable plan.
```

The skill may also activate automatically when the request closely matches its description, but explicit invocation is recommended for long, expensive research runs.

Useful context to provide:

- the project goal and the decision the research must support;
- research stage, available resources, and any existing implementation or measured results;
- unresolved questions or modules that would benefit from independent analysis;
- data/access, time, compute, and other relevant research constraints;
- local artifacts, repositories, papers, or prior conversations;
- any explicit override of the default GPT-6 Astra Pro web model;
- forbidden methods, such as Deep Research when it should not be used.

An explicit request to use the skill for a research task authorizes ordinary chats and focused follow-ups within that scope; there is no need to approve every send again. The destination must be unambiguous. A request only to edit the skill or draft prompts does not start a live research run. Sensitive data, uploads, sharing, and recurring monitoring retain their separate authorization requirements.

Platform references: [Codex Agent Skills](https://learn.chatgpt.com/docs/build-skills), [Kimi Code Agent Skills](https://www.kimi.com/code/docs/en/kimi-code-cli/customization/skills.html), and [Claude Code Skills](https://code.claude.com/docs/en/skills).

## Research and review principles

- **Evidence and novelty:** Inspect decision-critical primary sources and closest prior art. Separate direct evidence, transfer assumptions, concepts, and unsupported claims. A search that finds nothing does not prove an idea is new.
- **Discrimination and falsifiability:** Compare the leading idea with its strongest rival explanation and simplest credible baseline. Define the cheapest informative test and what would reverse the recommendation.
- **Stage-appropriate feasibility:** Check resource access, timeline, and scientific validity. Apply leakage, inference-input, calibration, tensor, and job-budget checks when the task actually involves them.
- **Consistency and critique:** Align the problem, gap, contribution, obtainable evidence, and defensible claim across workstreams. Preserve dissent rather than voting on model answers.
- **Bounded iteration:** Request narrow corrections with concrete counterexamples. Accept a decision, defer a gated claim, or reject a candidate when justified; additional complexity and self-scores are not evidence.

## Safety and privacy

- The reusable skill contains no credentials, cookies, account IDs, fixed project URLs, conversation IDs, or user-specific filesystem paths.
- It operates only through the user's own signed-in session and does not bypass subscriptions, access controls, or usage limits.
- It requires authorization before creating chats or sending messages.
- It never silently substitutes a different model.
- It never enables Deep Research unless the user explicitly requests it.
- Runtime research artifacts may contain user-supplied project links; keep those artifacts outside the reusable skill and review them before sharing.

## Limitations

- Web interfaces and model names change; selectors and verification steps may require maintenance.
- Long Pro responses can take tens of minutes and must be monitored without interruption.
- Browser access, login state, quotas, and model availability remain external dependencies.
- The final output supports a research decision; novelty and effectiveness remain provisional until the relevant source checks, proofs, or experiments establish them.

## Repository structure

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

## Disclaimer

This is an independent, unofficial Codex skill. It is not affiliated with or endorsed by OpenAI, ChatGPT, Google Chrome, or any model provider. Product names are used only to describe compatibility.
