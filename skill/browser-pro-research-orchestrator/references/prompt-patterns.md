# Prompt patterns

Use the shared contract plus the relevant mode's assignment. Replace placeholders with actual context before sending; remove inapplicable requirements. A prompt is a bounded research brief, not a command to produce maximum length. Ask for conclusions, evidence, concise rationale, calculations, and tests rather than a hidden chain-of-thought transcript.

## Shared initial contract

```text
You are a senior researcher in <domain>, responsible for <bounded question>.
The decision this analysis must support is <decision at current research stage>.

CONTEXT AND STATUS
<relevant self-contained context, with verified facts, source-reported claims,
assumptions, proposed work, unknowns, and provenance clearly separated>

CONSTRAINTS AND BOUNDARIES
<user priorities, resources, timeline, available/unavailable data, fixed decisions>
<neighboring workstream inputs/outputs only if relevant>
Address <scope>. Flag consequential problems outside it without redesigning them.

EVIDENCE
Use ordinary web search to verify primary papers or official source pages.
Do not activate Deep Research. If search/source access is unavailable, say so;
do not imply you searched or verified a citation.
For decision-critical sources provide title, year, task/population/data or
theoretical setting, relevant result, implication, limitation, and a direct
DOI, journal, PubMed, arXiv, or other primary-source link. Mark preprints.
Distinguish direct, transferable, conceptual, and unsupported evidence.
Separate what a source shows from your inference. Include closest prior art
and important negative or contradictory evidence; report evidence gaps.

ASSIGNMENT
<mode-specific assignment below>

DELIVERABLE
Give a clear recommendation or a justified decision to defer/reject, compared
with credible alternatives and the simplest appropriate baseline.
State the main uncertainty, strongest counterargument, what would reverse the
recommendation, and the cheapest informative next test with go/no-go criteria.
Do not invent measurements, exact resource counts, novelty, or consensus.
Use <output language> and detail proportionate to this decision.
```

If the user explicitly authorized Deep Research, update the tool instruction in every selected template, including follow-ups, only after resolving any conflict with exact-model requirements. If this is a pure reasoning revision with no new external claims, do not demand a repeated literature search.

## Direction assignment

```text
Develop a small set of scientifically distinct directions for <problem area>.
Start from important unresolved questions and the available resources, not a
preferred tool. For each, state the knowledge gain, closest prior art, possible
gap, access assumptions, principal risk, and first decisive investigation.
Compare importance, novelty headroom, tractability, resource fit, time to
evidence, and negative-result value under <priorities>.
Recommend a direction and useful backup; show when the ranking would change.
Do not design a complete pipeline before choosing the research question.
```

## Innovation assignment

```text
Develop candidate contributions addressing <bottleneck/question>.
Include distinct hypotheses or mechanisms, not just renamed combinations.
For each give the proposed contribution, why it could work, closest existing
work and exact difference, a testable prediction, strongest rival explanation,
minimal baseline/control, resources, and a falsifying result.
Search for prior work using synonyms and adjacent-field terminology, including
work that would make the claimed novelty disappear. Record search scope/date.
Rank the candidates and recommend the smallest experiment that distinguishes
the leading idea from its closest alternative. Novelty is provisional.
```

## Study assignment

```text
Turn <chosen question> into a study with a primary hypothesis or explicit
exploratory objective, coherent aims, and discriminating evidence.
Specify the appropriate protocol, data/participants/materials, controls,
measurement or proof strategy, analysis, and principal validity threats.
Separate confirmatory and exploratory work. Define what positive, negative,
and inconclusive results would mean for the claim.
State resource/access dependencies and sample-size or precision assumptions
when applicable. If inputs are unknown, propose pilot estimation or sensitivity
ranges instead of invented exact numbers. Include staged advance/pivot/stop
criteria and a minimal viable study.
```

## Pipeline assignment

```text
Design only <module> to serve <research hypothesis/evaluation objective>.
Respect <neighboring contracts> and the verified current baseline.
Compare plausible methods and a minimal credible baseline. Supply the needed
schemas/tensors, formulas, training/inference flow, state machine, and failure
behavior. Clearly label unavailable fields and quantities requiring code checks.
Bound compute and job counts, including folds, seeds, tuning, and calibration
when applicable. Audit leakage, inference-input availability, and attribution
of improvements. Give implementation stages, gates, and fallback behavior.
```

## Independent adversarial challenge

Use after initial independent generation. Give the critic the candidate and evidence, without calling it the winning or accepted answer.

```text
Critically assess this proposal for <decision> using the locked context below.
<context, proposal, evidence, known constraints>

First state its strongest faithful version. Seek the closest prior work,
strongest rival explanation, most fragile assumption, and experiment most
likely to disprove or sharply narrow the claim. Check whether a positive
result would actually distinguish it from the best simple alternative.
Use ordinary primary-source search for external claims; no Deep Research.
Separate fatal objections from fixable gaps and uncertainty. Do not invent
flaws to satisfy the critic role. Recommend retain/revise/reject and the
smallest discriminating next step; do not write an unrelated replacement plan.
```

## Focused revision

```text
Preserve <valid elements>. Resolve only these decision-blocking issues:
1. <claim/assumption/implementation error with evidence or counterexample>
2. <second blocker if needed>

<locked constraints and context changes since the previous prompt>
Do not repeat the full review or use Deep Research. Correct only the affected
hypothesis, comparison, protocol, equations, interface, or budget as applicable.
Add no new complexity without showing why it is necessary.
Return a short change memo: issue → correction → affected decision/test;
include the revised recommendation and remaining uncertainty. If a blocker
cannot be resolved, state which claim must be withdrawn or gated.
```

## Cross-workstream correction

```text
Two workstreams conflict on <specific issue>.
Contract/claim A: <exact definition and provenance>
Contract/claim B: <incompatible assumption and provenance>
Counterexample or consequence: <why this changes the research decision>

Provide a narrow correction preserving unrelated valid work. Align definitions,
revise the affected hypothesis/evaluation/interface, and state changes to
resources, dependent work, and the defensible conclusion. If the evidence
cannot resolve it, specify the discriminating test. No Deep Research.
```

For a clean restart, reuse the shared contract with current facts and a short factual list of invalid assumptions to avoid. Do not smuggle the previous recommendation in as a verified constraint.
