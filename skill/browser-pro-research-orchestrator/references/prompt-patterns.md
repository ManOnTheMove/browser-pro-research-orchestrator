# Prompt patterns

Use these patterns as scaffolding. Replace every angle-bracket placeholder with run-specific context. Do not send unexplained placeholders.

## Initial module research

```text
You are a senior methodological researcher in <domain>.

Conduct an ordinary web-based literature search and design <module>.
Do not use Deep Research. Verify primary papers or official publication pages;
do not cite from memory alone.

PROJECT GOAL
<goal>

VERIFIED CURRENT SYSTEM
<implementation, metrics, interfaces>

HARD CONSTRAINTS
<data size, compute, leakage, deployment, forbidden approaches>

NEIGHBORING MODULE INTERFACE
<inputs received and outputs required>

ONLY TOPIC
Address only <module>. Do not redesign <neighboring module>.

LITERATURE REQUIREMENTS
- Prioritize direct evidence, then transferable evidence.
- Label conceptual-only evidence.
- For every key paper provide title, year, task/data, method, implication,
  limitation, and a primary-source link.
- State explicitly when direct evidence is absent.

TECHNICAL REQUIREMENTS
<alternatives, tensors, formulas, losses, state machine, evaluation>

FEASIBILITY
- Include a low-complexity baseline.
- Give exact added parameters or a code-verification plan.
- Give exact model/job counts.
- Define staged go/no-go criteria and fallback behavior.

OUTPUT
1. evidence map;
2. factual discrepancies;
3. compared alternatives;
4. one recommended primary design;
5. one minimal baseline;
6. exact implementation contract;
7. leakage-safe evaluation;
8. unresolved facts and kill criteria.
```

## Focused revision

```text
The response has useful elements, but it is not yet accepted.
Do not repeat the literature review. Do not use Deep Research.

KEEP
<strong parts>

RESOLVE THESE BLOCKERS
1. <specific inconsistency or counterexample>
2. <feasibility or leakage problem>
3. <interface or calibration problem>

REQUIRED REVISION
- Change only the affected formulas, modules, pseudocode, and job table.
- Remove unearned complexity.
- Align training targets with inference decisions.
- Use only fields available at inference.
- Preserve the neighboring module's ownership boundary.
- End with one revised design and an honest scored self-audit.
```

## Cross-module corrigendum

```text
The individual module design is close to acceptable, but the integrated
interface has a contradiction.

UPSTREAM CONTRACT
<exact field definitions>

DOWNSTREAM ASSUMPTION
<exact conflicting definition>

COUNTEREXAMPLE
<case showing unsafe or undefined behavior>

Provide a short corrigendum that:
- versions or renames the conflicting fields;
- aligns training and inference semantics;
- corrects the state machine;
- changes no unrelated modules;
- adds no new learned head unless strictly necessary;
- states whether model/job counts change.
```

## Restart prompt

Use a new chat when the old one has drifted:

```text
Independently solve <module> from the following locked context.
Do not inherit conclusions from other chats unless they are listed as verified
constraints below. Do not use Deep Research.

<fresh context packet>

The prior direction was rejected because:
<short failure list>

Develop a simpler, falsifiable alternative and compare it with the minimal
baseline before recommending a final design.
```
