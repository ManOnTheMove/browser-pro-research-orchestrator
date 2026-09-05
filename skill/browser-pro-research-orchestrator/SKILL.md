---
name: browser-pro-research-orchestrator
description: Use browser-based ChatGPT GPT-6 Pro to investigate research directions, develop and challenge novel ideas, design studies, and build research pipelines. Coordinate independent Pro conversations through signed-in Chrome, verify the selected model, scrutinize primary evidence, and synthesize a defensible research decision. Use for deep research-project reasoning with the web Pro model, including projects with no code or dataset yet; not for unrelated brainstorming or routine implementation.
---

# Browser Pro Research Orchestrator

Turn a difficult research question into a defensible decision and an actionable next experiment. The local orchestrator owns the scientific reasoning, context, critique, and synthesis; browser Pro conversations supply independent analyses and challenges.

## Model contract

- **Default browser target: ChatGPT GPT-6 Pro — GPT-6 Astra with Pro selected.** The user's names `ChatGPT-6 Pro`, `GPT-6 Pro`, and `GPT-6 ASTRA PRO` express this target. They are not promises about literal UI labels or API model IDs.
- **Expected local orchestrator: GPT-6 Astra, Ultra reasoning.** Treat this as the user's operating assumption. Use the local model for substantial reasoning and adjudication, not just forwarding prompts. Do not change local settings, map Ultra to a web mode/API parameter, or claim the running model was verified when it was only assumed.
- A later explicit user model choice overrides the default for that run. Otherwise require the GPT-6 Astra family **and** Pro mode before every browser send. Never silently substitute GPT-5.6 Pro, Thinking, Auto, Instant, or another model.
- Resolve displayed names from the live model controls. A subscription badge saying Pro, a conversation title, a model's self-description, or an API model listing does not verify the selected web model.

## Scope, access, and authority

Use an available browser connector that can operate the user's signed-in Chrome session. Follow its actual documentation; do not assume a named Chrome skill or a fixed selector exists. Keep the requested browser and account context.

An explicit request to use this skill for a research task authorizes the ordinary research conversations and focused follow-ups necessary within that scope. Reuse existing authorization rather than asking before every send. Merely editing this skill or drafting prompts does not authorize a live research run. Respect separate authorization requirements for sensitive data, uploads, sharing, or actions outside the research scope.

Discover the intended ChatGPT project/workspace from the user's instructions and visible context. Ask only if the destination remains ambiguous. A dedicated web project is optional: an unambiguous ordinary chat destination is sufficient. Do not create a project as a prerequisite. Missing code or data is valid in early research; record it instead of blocking ideation.

If login, Chrome access, the intended destination, or exact model verification is unavailable, stop dependent browser sends and name the blocker. Continue useful local preparation, clearly labeled as such; do not report an unperformed Pro consultation as complete.

## 1. Frame the decision and select the research mode

Capture the scientific problem, decision to make now, research stage, relevant artifacts, known resources, deadline, and desired output. Separate user requirements from tentative assumptions. Ask for missing information only when it could change the recommendation; otherwise proceed with explicit assumptions and sensitivity analysis.

Read the relevant sections of [references/research-modes.md](references/research-modes.md):

| Mode | Use when the user needs | Main deliverable |
|---|---|---|
| Direction | A research topic or choice among directions | Ranked shortlist, recommendation, decisive next investigation |
| Innovation | Defensible contributions or new hypotheses | Novelty candidates, closest prior art, falsification tests |
| Study | A research question turned into a study/project | Aims, hypothesis, protocol, analysis, staged feasibility gates |
| Pipeline | A chosen research goal turned into a method/system | Minimal baseline, interfaces, evaluation, implementation plan |
| Challenge | A proposed direction/design critically assessed | Strongest objections, evidence gaps, revision or rejection |

Combine modes only when the current decision requires it. A full lifecycle can proceed Direction → Innovation → Study → Pipeline, but do not force every request through every stage. Do not require tensors, losses, deployed inference, or code for a question that is not about them.

Before reading Pro conclusions, write a compact local provisional analysis: candidate explanations/directions, important unknowns, likely confounders, decision criteria, and what evidence could reverse the current view. Hold back the local preferred answer from independent discovery prompts unless it is a user-imposed constraint.

## 2. Lock context and choose independent workstreams

Inspect relevant local artifacts and existing conversations. Use a versioned context packet with these distinctions:

```text
USER GOALS AND HARD CONSTRAINTS
VERIFIED LOCAL FACTS / MEASURED RESULTS
REPORTED BY PRIMARY SOURCES
INFERRED BUT NOT VERIFIED
PROPOSED FUTURE WORK
UNKNOWNS / UNAVAILABLE RESOURCES / OUT OF SCOPE
```

Attach provenance to decision-critical facts. Never turn a paper result, user estimate, planned dataset, or repository aspiration into a measured local result. Include the relevant content in each prompt; the web model cannot read an unexplained local path. Minimize material transmitted to what the task needs.

Decompose by **decision uncertainty**, not necessarily by software module. Useful workstreams include opportunity/prior-art search, alternative hypotheses, study design, feasibility, adversarial critique, or a bounded technical module. Record each one's question, inputs, deliverable, dependencies, and acceptance criteria.

Use the smallest useful set: often one conversation for a narrow question, two to four for a difficult open decision. Add another only when it resolves a distinct uncertainty. Dispatch independent initial chats before sharing their conclusions; send dependent design work only after its prerequisites are settled. A browser conversation is not a new Codex task.

Separate conversations reduce conversational anchoring, but shared model training and project memory can still correlate outputs. Record known shared context, provide self-contained prompts, and do not treat agreement as independent scientific evidence. Do not alter account memory settings to manufacture independence.

Set a practical run budget for initial conversations, revision rounds, and elapsed time. Unless the task calls for more, use up to two focused revision rounds per workstream, then decide whether new evidence justifies another, a fresh chat is warranted, or the candidate should be rejected/deferred. More text or agreement alone is not progress.

## 3. Prepare prompts and send with verified model selection

Read [references/prompt-patterns.md](references/prompt-patterns.md) for the shared prompt contract and the pattern matching the chosen mode. Ask for primary-source research, alternatives, a substantive recommendation, explicit uncertainties, and tests capable of disproving the proposal. Use the user's language for the final synthesis; use another prompt/search language only when useful, without assuming English inherently improves reasoning.

Ordinary web search is the default. **Do not activate Deep Research unless the user explicitly requests it.** A request for deep thinking is not a request for that product mode. If explicitly requested Deep Research conflicts with the exact model requirement, resolve that conflict rather than silently switching modes. Follow-up prompts inherit the same tool constraints.

Read [references/browser-protocol.md](references/browser-protocol.md) before the first browser send or when resuming a run. It governs exact model verification, safe submission, long waits, answer capture, and recovery. Verify every initial prompt, revision, and retry; prompt text naming GPT-6 cannot select a model.

## 4. Review, challenge, and revise

Read [references/review-rubric.md](references/review-rubric.md) before accepting a recommendation. Apply common scientific gates and only the domain/stage-specific checks that fit the task.

Locally verify decision-critical citations by opening primary sources and inspecting the relevant methods/results, including the closest prior art and evidence supporting the central claim. A browser Pro answer is a research input, not verification. If a source is inaccessible, label the limitation and withhold claims that depend on inaccessible details. Recalculate important quantities or inspect code/data when available.

Classify each workstream as `ACCEPT`, `CONDITIONAL ACCEPT`, `REVISE`, `RESTART`, or `REJECT`. Acceptance means sufficient to support the stated next research decision, not proof of novelty, effectiveness, or publication prospects. A conditional acceptance must state the unresolved condition, how to test it, and what action remains gated.

For revision, retain valid parts, enumerate blocking errors with evidence/counterexamples, and request only the affected changes. Use corrected hypotheses, controls, comparisons, or decision criteria for conceptual work; use equations, interfaces, and job counts when technical work requires them. Restart a drifted conversation with refreshed facts; do not restart merely because its conclusion is unfavorable.

For consequential direction or novelty decisions, obtain a serious adversarial pass. Use a separate browser critic when it can add an independent analysis; otherwise perform and label the local critique. Compare the strongest case for and against the leading candidate. Preserve substantive dissent and resolve it with evidence or a discriminating experiment, not majority vote or self-scores.

## 5. Audit consistency and synthesize the research decision

Audit the full claim chain at the level appropriate to the task:

```text
important problem → documented gap → proposed contribution/hypothesis
→ obtainable evidence → discriminating evaluation → defensible claim
```

Check that population, objective, assumptions, resource access, contribution, controls, success criteria, and timeline agree across workstreams. For pipelines, also audit field ownership, units/shapes, training/inference availability, missingness, calibration, refits, and combined job budgets using the rubric. Apply a single-workstream consistency check when there are no cross-stream interfaces.

Send a narrow correction when a contradiction changes the recommendation. If evidence cannot settle it, make the uncertainty and its effect on the decision explicit; do not quietly merge incompatible proposals.

Lead the final synthesis with the recommendation, rationale, confidence, and what would change it. Include only the relevant mode-specific deliverables, plus:

- the locked facts and material assumptions;
- the strongest alternative and why it lost under the stated criteria;
- evidence for the gap/contribution, nearest prior art, and limits of novelty claims;
- the cheapest informative next step, staged plan, resources, and go/no-go or pivot criteria;
- unresolved disagreements and dependencies;
- traceable primary-source citations, web conversation links, and local artifacts.

A defensible conclusion may be to abandon a candidate, obtain a missing measurement, or narrow the question. Do not force a positive recommendation. Distinguish a completed research decision from an implemented or experimentally validated result.

## Run records, resumption, and completion

Store runtime artifacts in a neutral workspace-relative folder such as `pro-research/<run-slug>/`. Maintain `context-lock.md`, `local-analysis.md`, `run-log.md`, and `final-synthesis.md`, plus `workstream-<name>-prompt-v<n>.md`, `workstream-<name>-response-v<n>.md`, and `workstream-<name>-review-v<n>.md` for actual exchanges. Keep a compact claim-to-source ledger in the run log or a separate `evidence-ledger.md` when substantial.

Record each conversation's observed link, context/prompt version, verified model/mode, verification time and UI evidence, send status/time, answer capture status, review decision, and next action. Track any monitor identifier and scheduled check time. Runtime links may be private; reusable skill files must remain project-agnostic.

Track state per workstream: `PREPARED → VERIFIED → SENT → WAITING → CAPTURED → REVIEWED`, followed by a focused revision loop or an explicit acceptance/rejection. Overall states are `FRAMING`, `RESEARCHING`, `REVIEWING`, `SYNTHESIZING`, and `COMPLETE`; record a browser blocker without discarding local progress. On resume, read these artifacts and inspect the existing conversation before sending anything again.

Complete a browser-assisted run only when required responses are fully captured with verified target provenance, blocking objections are resolved or the affected recommendation is explicitly rejected, and the consistency audit and synthesis are finished. If a past send used the wrong or unverified model, retain that error in the log, exclude the response from the required Pro evidence, and complete any necessary replacement consultation before claiming success. Explicit user cancellation can close outstanding work; elapsed budget alone does not turn an unanswered required chat into a completed consultation. Report partial work honestly. Stop only monitors created for this run once they are no longer needed.

For an explicit prompt-only or local-preparation request, deliver the reviewed prompts/context and their remaining prerequisites. That requested preparation can be complete without a browser run; do not describe it as completed Pro research.

Keep credentials, cookies, tokens, account names, fixed project URLs/IDs, conversation IDs, and user-specific paths out of the reusable skill. Read destination details at runtime. Preserve user-owned tabs and unrelated browser state.
