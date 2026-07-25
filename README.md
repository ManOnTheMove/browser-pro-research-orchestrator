# Browser Pro Research Orchestrator

**English** · [简体中文](README.zh-CN.md) · [Français](README.fr.md)

Turn a signed-in browser session and a web-only Pro model into a panel of slow, independent research specialists—while Codex remains the orchestrator, reviewer, and final decision maker.

![Browser Pro Research Orchestrator research pipeline](docs/browser-pro-research-orchestrator.png)

## Why this skill exists

Complex projects rarely fail because one idea is missing. They fail because several difficult modules must be researched independently, their assumptions must agree, and the resulting design must still fit the available data, compute, interfaces, and deployment constraints.

Web-only Pro models can provide unusually broad and deep analysis, but a single long conversation is a poor substitute for coordinated research. It tends to mix modules, lose constraints, and accept its own proposals too easily.

This Codex skill supplies the missing orchestration layer.

## What it does

- decomposes a complex project into two to five bounded research modules;
- creates separate Pro conversations through the user's existing signed-in Chrome session;
- verifies the selected project, model, and reasoning mode before every send;
- drafts context-rich prompts that request ordinary web research and primary evidence;
- waits for long responses without clicking **Answer now** or degrading the result;
- reviews every proposal for evidence quality, leakage, feasibility, complexity, and operational cost;
- sends focused revision prompts or restarts a drifting thread;
- audits interfaces and responsibilities across modules;
- synthesizes an implementable, falsifiable design with go/no-go gates and fallbacks.

The workflow is domain-general. It can support software architecture, computer vision, machine learning, scientific pipelines, systems engineering, product design, and other multi-module research tasks.

## How it works

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

The Pro model is treated as a research proposer, not an authority. A module is accepted only after its evidence, assumptions, compute budget, evaluation protocol, failure modes, and interfaces are reviewable.

## Installation

Copy the packaged skill into your Codex skills directory:

```bash
cp -R skill/browser-pro-research-orchestrator ~/.codex/skills/
```

Then restart or reopen Codex so the skill catalog refreshes.

## Requirements

- Codex with a Chrome-control integration or equivalent browser connector;
- an existing signed-in browser session with access to the requested web model;
- user authorization to create conversations and send prompts;
- a clearly identified target project/workspace and exact model mode.

The skill does not provide a subscription, credentials, browser login, or model access.

## Usage

Invoke the skill explicitly:

```text
Use $browser-pro-research-orchestrator to decompose this complex project,
run independent Pro research chats through Chrome, review them critically,
and synthesize a feasible implementation plan.
```

Useful context to provide:

- the project goal and the decision the research must support;
- current implementation and measured results;
- modules that should be researched independently;
- hard data, compute, latency, and deployment constraints;
- local artifacts, repositories, papers, or prior conversations;
- the exact web model and reasoning mode;
- forbidden methods, such as Deep Research when it should not be used.

## Research and review principles

### Evidence before novelty

Prompts request primary sources and distinguish direct evidence from transferable or conceptual-only evidence. Unsupported gaps remain explicit.

### Feasibility before sophistication

Every proposal is checked for data leakage, unavailable inference inputs, excessive thresholds or losses, unbounded job counts, hidden manual steps, and missing failure cases.

### Interfaces before synthesis

The final cross-audit checks identities, units, tensor shapes, missing-value semantics, threshold ownership, calibration, retry and abstention behavior, artifact provenance, and training-versus-inference fields.

### Iteration before acceptance

Weak designs receive narrow corrigenda with concrete counterexamples and requested equations, pseudocode, interfaces, or budgets. A new conversation is used when a thread has accumulated contradictory assumptions.

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
- The final output is a research design, not proof of empirical improvement. Implementation and evaluation are still required.

## Repository structure

```text
.
├── README.md
├── README.zh-CN.md
├── README.fr.md
├── docs/
│   └── browser-pro-research-orchestrator.png
└── skill/
    └── browser-pro-research-orchestrator/
        ├── SKILL.md
        ├── agents/
        │   └── openai.yaml
        └── references/
            ├── prompt-patterns.md
            └── review-rubric.md
```

## Disclaimer

This is an independent, unofficial Codex skill. It is not affiliated with or endorsed by OpenAI, ChatGPT, Google Chrome, or any model provider. Product names are used only to describe compatibility.
