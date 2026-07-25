---
name: browser-pro-research-orchestrator
description: Orchestrate complex project-architecture research through a logged-in Chrome session by running multiple independent ChatGPT Pro conversations, waiting for long responses, critically reviewing and iterating them, auditing cross-module interfaces, and synthesizing an evidence-backed implementable design. Use when Codex cannot call the requested Pro web model directly and a project has multiple difficult or interdependent modules that need literature research, parallel chats, iterative critique, or browser-verified model selection.
---

# Browser Pro Research Orchestrator

Use a browser-accessed Pro model as a panel of slow, independent research specialists while retaining Codex as the orchestrator, reviewer, and final decision maker.

Do not treat the Pro model as an authority. Treat every response as a research proposal that must pass evidence, feasibility, leakage, and interface review.

## Required capabilities and authority

1. Use the Chrome-control skill or equivalent browser connector that can access the user's existing signed-in Chrome session.
2. Require the user to identify the target web project/workspace and target model, or use the active page only when its identity is unambiguous.
3. Obtain authority before creating conversations, sending prompts, or sending follow-ups. One explicit authorization may cover later writes within the same stated research scope.
4. Never store credentials, cookies, account identifiers, fixed project URLs, conversation IDs, or user-specific filesystem paths in this skill.
5. If Chrome control, login state, project access, or the exact requested model is unavailable, stop and report the precise blocker. Do not silently substitute another model.

## Run state machine

Track the run through these states:

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

Use `BLOCKED` only when a required capability, authorization, login, or model is unavailable. Re-enter `WAITING` after every follow-up.

## 1. Discover and bound the task

Capture:

- the project goal and decision that the research must support;
- the complex modules or questions;
- dependencies and interfaces between modules;
- verified constraints, resource limits, sample size, and deployment conditions;
- local files, repositories, datasets, papers, and existing conversations;
- the exact web model and reasoning mode requested;
- actions already authorized by the user;
- forbidden tools or methods, such as Deep Research when excluded.

If the user has not decomposed the project, propose the smallest set of independently researchable modules. Create one Pro conversation per module. Keep shared interfaces explicit, but avoid placing all modules in one prompt merely because they interact.

Prefer two to five bounded module chats. Add a separate cross-module audit chat only when the interfaces are themselves a major research problem.

## 2. Build and lock the context packet

Inspect the relevant local artifacts and existing web conversation before prompting the Pro model.

Create a compact context packet containing:

- verified current implementation;
- measured results;
- paper or dataset claims that differ from the implementation;
- known failure modes;
- missing artifacts and unimplemented capabilities;
- hard scientific and engineering constraints;
- facts that remain uncertain;
- work that the user explicitly says is obsolete or out of scope.

Separate these categories:

```text
MEASURED IN THE CURRENT SYSTEM
REPORTED BY A PAPER OR DATASET
INFERRED BUT NOT VERIFIED
PROPOSED FUTURE WORK
```

Never let a paper result, manual-input result, or repository aspiration become a measured result of the current system.

Store run artifacts under a neutral workspace-relative directory such as:

```text
pro-research/<run-slug>/
```

Use generic filenames:

```text
context-lock.md
module-<name>-prompt.md
module-<name>-review.md
run-log.md
final-synthesis.md
```

Runtime artifacts may contain user-provided links when needed for that run. The reusable skill itself must not.

## 3. Design independent research prompts

Read [references/prompt-patterns.md](references/prompt-patterns.md) when drafting or revising prompts.

Default to English when it improves technical search and model performance, unless the user requests another language.

Every initial module prompt must include:

1. a domain-expert role;
2. the full relevant context packet, not unexplained local references;
3. a single bounded topic;
4. an instruction to conduct ordinary web research and verify primary sources;
5. a clear statement that Deep Research is forbidden unless the user requested it;
6. current implementation facts and non-negotiable constraints;
7. literature evidence tiers and an explicit evidence-gap requirement;
8. architecture or method alternatives, including a low-complexity baseline;
9. leakage, compute, sample-size, and deployment constraints;
10. exact tensors, interfaces, losses, state machines, job counts, or other implementable details appropriate to the topic;
11. falsifiable go/no-go criteria;
12. a required final recommendation rather than an unranked list.

Ask for primary-paper title, year, task/data, method, direct implication, limitation, and DOI/PubMed/journal/arXiv link. Require the model to label direct, transferable, and conceptual-only evidence.

Do not ask the model to redesign another module inside a module-specific chat. Supply the neighboring module's interface as a constraint instead.

## 4. Verify the exact web model before every send

Use the user's signed-in Chrome session.

Before each new conversation or follow-up:

1. confirm the page belongs to the intended project/workspace;
2. open the model controls;
3. verify the requested reasoning mode is selected, such as `Pro`;
4. verify the exact requested model is selected;
5. close the menus without changing the selection;
6. take a fresh page snapshot before locating the prompt box;
7. ensure the prompt box and send control resolve uniquely;
8. send only the reviewed prompt;
9. verify the message is visible and generation has started.

Do not infer the model from a conversation title or prior state. Verify the checked UI items.

Never:

- click `Answer now`;
- enable Deep Research unless explicitly requested;
- interrupt a long Pro response because it appears slow;
- reuse one conversation for independent modules merely to save time;
- send a follow-up to the wrong project or model.

When the browser-control skill requires tab finalization, make tab finalization the last Chrome operation of the turn.

## 5. Wait without degrading the response

Pro responses may take tens of minutes.

- Do not use a blocking shell sleep.
- Use a heartbeat, monitor, or scheduled follow-up when available.
- Default to checking after about 15–20 minutes unless the UI gives a better estimate.
- If `Stop answering` or equivalent is present, leave the response untouched and schedule another check.
- If `Answer now` appears, do not click it.
- When the response completes, read the entire answer, not only the visible tail or executive summary.
- Record the elapsed time and conversation link in the run log.

Do not report completion while any required module response or review is unfinished.

## 6. Review every response as a skeptical methodologist

Read [references/review-rubric.md](references/review-rubric.md) before accepting a design.

Check:

- whether cited evidence is direct or merely analogous;
- whether facts match the current implementation;
- whether training, tuning, calibration, and test data leak into one another;
- whether compute and job counts are operationally bounded;
- whether the design has too many features, thresholds, heads, losses, or calibrators for the data;
- whether failure cases remain in the denominator;
- whether abstention has a valid target rather than a relabeled proxy;
- whether the proposed inference inputs exist and contain no ground truth;
- whether parameter counts and tensor interfaces are code-verifiable;
- whether simpler baselines can isolate the claimed contribution;
- whether the design defines kill criteria and a fallback method.

Classify each module:

```text
ACCEPT
CONDITIONAL ACCEPT
REVISE
RESTART IN A NEW CHAT
REJECT
```

Do not accept a high self-score as evidence.

## 7. Send focused revision prompts

When revision is needed:

1. preserve the strong parts explicitly;
2. enumerate only the blocking errors;
3. show concrete counterexamples or inconsistent formulas;
4. demand corrected equations, tensor flow, pseudocode, thresholds, and job counts;
5. limit new degrees of freedom;
6. require a short revision memo rather than a repeated literature review;
7. retain the same model, project, and module scope.

Start a new chat when the conversation has drifted, accumulated contradictory assumptions, or repeatedly ignores the same hard constraint.

Return to `WAITING` after every send. Iterate until the design is implementable and falsifiable, not until it merely sounds sophisticated.

## 8. Perform a cross-module interface audit

After the module chats pass individually, compare them side by side.

Audit:

- shared entity/group/item identity;
- units, coordinate systems, tensor shapes, and missing-value semantics;
- overloaded terms such as `usable`, `partial`, `confidence`, or `evidence`;
- thresholds that use different definitions across modules;
- which module owns ranking, retry, fallback, calibration, and abstention;
- training versus inference fields;
- shared cross-fitting manifests and artifact provenance;
- distribution shift introduced by final refits;
- whether separate job budgets are additive or reusable;
- whether two modules independently reject the same case;
- whether a downstream module assumes an upstream field that is not produced.

Rename conflicting fields or version the interface instead of relying on prose.

If the interface audit reveals a hard contradiction, send a narrow corrigendum to the responsible module chat. Do not hide the contradiction in the final synthesis.

## 9. Synthesize the implementation plan

Produce a final report that contains:

1. the decision and confidence level for each module;
2. the verified baseline and factual discrepancies;
3. the recommended method and minimal baseline;
4. exact interfaces and responsibility boundaries;
5. staged implementation order;
6. shared and additive compute budgets;
7. go/no-go gates and fallback methods;
8. leakage-safe evaluation;
9. unresolved data or code facts;
10. prohibited over-designed alternatives;
11. key primary literature;
12. links to the created web conversations and local prompt artifacts.

Lead with the outcome. State clearly that an accepted design is a research plan, not a measured improvement.

## Completion criteria

Mark the run complete only when:

- every required module has a complete Pro response;
- the exact requested model was verified for every send;
- all blocking review items were resolved or explicitly rejected;
- the cross-module interface audit passed;
- the final synthesis distinguishes measured facts from proposals;
- the user can trace prompts, conversations, revisions, and decisions;
- any recurring monitor created for the run has been stopped.

## Privacy and portability

- Keep the skill project-agnostic.
- Read project links and filesystem paths only at runtime.
- Do not write cookies, tokens, account names, project IDs, or conversation IDs into reusable files.
- Do not assume a fixed ChatGPT URL structure.
- Do not claim compatibility with another browser agent unless it can perform the same checked UI operations.
- Preserve user-owned tabs and unrelated browser state.
