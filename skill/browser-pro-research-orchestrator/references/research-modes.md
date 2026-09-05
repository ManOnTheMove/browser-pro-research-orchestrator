# Research modes

Read only the mode(s) relevant to the current decision. Adapt the level of detail to research maturity; mark unavailable inputs as unknown and avoid invented measurements. Candidate counts below are useful starting points, not quotas.

## Direction: choose a question worth pursuing

Start from the important unresolved problem and the user's actual advantages: data access, methods, collaborators, domain expertise, equipment, time, and scientific interests. A repository is optional. Separate a dataset already accessible from one merely expected to become available.

1. Map the problem landscape, dominant approaches, unsettled assumptions, contradictory results, and underserved settings. Distinguish scientific importance from a fashionable technique.
2. Generate a small set of materially different directions, often three to five. Vary the question or explanation, not just the architecture name.
3. Give each candidate a one-sentence question, intended knowledge gain, closest prior work, plausibly open gap, required resources, main failure risk, and first informative investigation.
4. Compare importance, novelty headroom, tractability, resource fit, time to decisive evidence, and value even under a negative result. State the user's priorities before ranking. Use qualitative judgments or explicit weights; show whether plausible changes in priorities alter the winner. Do not manufacture precision from arbitrary scores.
5. Recommend a primary direction and, when useful, a backup. Explain what evidence would reverse the ranking. If none is currently viable, recommend the specific scoping work needed before commitment.

Output a direction memo: ranked shortlist, decision rationale, assumptions, nearest prior work, and a bounded next investigation. Do not force a full system design before the research question is chosen.

## Innovation: develop and test a contribution claim

Create candidate innovations from an observed failure, untested mechanism, inconsistent evidence, unmet requirement, useful measurement, or changed scientific question. Method, theory, dataset, experimental protocol, evaluation, and empirical finding can all be contributions when justified.

For each candidate, make an innovation card:

```text
Question and current bottleneck
Candidate contribution in one sentence
Mechanism or explanation: why this should change what we can learn/do
Closest prior art and the exact overlap/difference
New testable prediction or observable consequence
Simplest baseline, competing explanation, and decisive comparison
Required data/resources and unverified assumptions
Failure result that would invalidate or sharply narrow the claim
Value and next action if the proposed effect is absent
```

Use separate generation and disconfirmation passes. Search the proposed idea and its underlying mechanism under synonyms, established terminology, adjacent disciplines, and the closest cited/citing work when accessible. Include older foundations as well as recent work; new terminology does not establish a new idea.

Distinguish novelty from utility, feasibility, and evidence of efficacy. A new combination can be worthwhile only if the interaction yields a specific nontrivial hypothesis or demonstrated benefit beyond its components. Require the relevant factorial comparison or ablation rather than rewarding added modules.

Record novelty-search date, search scope/queries, closest work, and access limits. Use calibrated language such as “candidate contribution not located in the searched sources.” Do not claim “first,” “never studied,” guaranteed publication, or a vacant field because a few searches found nothing. Lack of direct supporting evidence does not itself invalidate a new hypothesis; the mechanism and test must remain defensible.

Output a small ranked set of innovation cards, the strongest counterargument to the leader, and a minimum experiment that separates the proposed explanation from the nearest alternative.

## Study: turn a question into discriminating evidence

Translate the chosen question into a primary hypothesis or precise exploratory objective and coherent aims. Define what each aim establishes and whether later aims depend on it. Do not treat a collection of techniques as aims.

Choose details appropriate to the discipline:

- Empirical/interventional work: target population, sampling and unit of analysis, variables, comparators/controls, intervention or exposure, endpoints, bias/confounding, missingness, exclusions, and analysis.
- Computational work: datasets and provenance, label/input availability, splits, realistic baselines, robustness/shift tests, leakage controls, resource accounting, and reproducibility.
- Theoretical work: definitions, assumptions, conjectures, smallest nontrivial cases, proof obligations, counterexample search, and relation to established results.
- Qualitative or mixed work: research question, recruitment/access, sampling rationale, data collection, analysis approach, reflexivity, credibility checks, and integration of evidence.

Separate confirmatory hypotheses from exploratory analyses. Define the smallest scientifically meaningful effect or other success criterion and the assumptions needed for precision/power planning when applicable. If effect sizes, variance, or access are unknown, specify pilot estimation and sensitivity ranges rather than inventing an exact sample size. Preserve uncertainty and negative outcomes.

Identify actual recruitment, annotation, equipment, collaborator, data-permission, or ethics dependencies when they determine feasibility. Planning a study does not authorize recruitment or experimentation. Keep these checks specific to the proposed study.

Output a study blueprint with aims, protocol, comparisons, analysis, estimated resources/timeline with assumptions, risks, a minimal pilot, and advance/pivot/stop criteria. State which conclusions the design can and cannot support.

## Pipeline: operationalize a chosen research objective

Confirm that the scientific question and evaluation contract are settled enough to constrain engineering. Inspect the actual baseline and artifacts. Separate current implementation from intended capability.

Use one bounded conversation per separable difficult module when useful. Provide neighboring contracts as constraints; ask each module to state interface problems without redesigning everything.

Require implementable detail where relevant: input/output schemas and tensors, units, preprocessing, labels, equations, losses, train/inference pseudocode, state transitions, failure behavior, parameter-verification plan, and job/compute estimates. Mark code-dependent quantities as estimates until inspected or measured.

Plan from a minimal credible baseline through the smallest change that tests the contribution. Add modules only when a prespecified residual failure motivates them. Audit cross-fitting, calibration, fallback ownership, final refits, and the total integrated compute cost using the review rubric.

Output a method specification with contracts, implementation order, contribution-isolating experiments, validation gates, fallback, and unresolved code/data facts. A good pipeline supports the study's scientific claim rather than becoming the claim by default.

## Challenge: assess an existing proposal

First state the strongest faithful version of the proposal. Evaluate the claim, not the author's confidence or preferred terminology.

Check closest prior art, rival explanations, resource assumptions, falsifiability, flawed comparisons, impossible data access, and whether a positive result would actually support the claimed conclusion. For pipelines, add implementation and interface checks.

Rank objections by effect on the decision: fatal, resolvable before commitment, or worth monitoring. Distinguish an absence of evidence from evidence against the idea. Avoid manufacturing objections merely to sound critical.

Output an accept/revise/reject judgment with evidence, the smallest necessary changes, and the single most informative next test. Preserve useful elements without insulating the central claim from disconfirmation.
