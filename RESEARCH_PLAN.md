# Research Plan

## Central question

Can multi-agent disagreement and evidence consistency quantify uncertainty in biomedical drug reasoning well enough to support calibrated abstention?

The first claim to test is intentionally weaker and falsifiable:

> Inter-agent disagreement predicts DrugAgent errors and adds useful information beyond simple confidence / vote / evidence baselines.

Do not proceed to learned abstention policies until this survives.

## Phase 0 — Identifiability and data audit

Before generating anything expensive, establish what outputs are available and whether error labels can be defined.

Audit:

- number of cases;
- number and roles of agents;
- whether per-agent answers are available;
- whether per-agent confidence exists;
- whether retrieved evidence / citations are available;
- final aggregate answer;
- gold/verified outcome or other defensible correctness label;
- parsing failure rate;
- class balance;
- repeated templates / questions / entities;
- whether examples are sufficiently independent for grouped evaluation.

If the only way to define correctness is by the same model's self-judgment, document this as a major limitation and seek a stronger label before interpreting uncertainty results.

### Gate 0

Proceed only if there is a defensible correctness target and enough cases to estimate error detection without obvious leakage.

Otherwise `PIVOT` or report a blocker.

## Phase 1 — Cheap retrospective disagreement test

Compute transparent disagreement scores from existing agent outputs, for example:

- fraction disagreeing with final answer;
- vote entropy;
- majority margin;
- pairwise disagreement;
- answer diversity;
- mechanistic/evidence inconsistency if directly measurable.

Do not learn a complex uncertainty model.

Ask:

1. Are errors more common when agents disagree?
2. Is the relationship monotonic?
3. Does disagreement detect errors better than chance?
4. Is it stable across question types / drug classes / templates where available?

Report effect sizes and uncertainty, not just p-values.

### Gate 1

If disagreement has no meaningful relationship with errors, `KILL` the core disagreement hypothesis.

## Phase 2 — Embarrassingly simple baselines

Compare disagreement against:

- aggregate confidence;
- best/single-agent confidence;
- majority-vote margin;
- vote entropy (if not already the main score);
- evidence count;
- evidence coverage / missing evidence;
- question length / number of entities where relevant;
- answer prevalence;
- simple OOD indicators.

Then test incremental value:

`error ~ simple_baselines`

versus

`error ~ simple_baselines + disagreement`

Use held-out or cross-validated evaluation rather than in-sample fit.

### Gate 2

If disagreement adds no reproducible incremental value, prefer `GO-NARROW`, `PIVOT`, or `KILL` rather than adding architecture complexity.

## Phase 3 — Selective prediction

Turn the uncertainty signal into an abstention ranking without training a complex policy.

For each uncertainty method, evaluate:

- risk-coverage curve;
- selective risk;
- retained accuracy as coverage decreases;
- error enrichment among rejected cases;
- calibration / reliability where appropriate.

Do not cherry-pick a single threshold.

The practical question is:

> If the system abstains on the least-trusted cases, does error among answered cases reliably fall faster than with simpler confidence baselines?

### Gate 3

A positive scientific result requires a meaningful, reproducible selective-prediction benefit.

## Phase 4 — Falsification controls

Try to explain disagreement away.

At minimum diagnose:

- question difficulty;
- agent count;
- one systematically weak agent;
- low confidence common to all agents;
- explicit conflict in retrieved evidence;
- prompt/template identity;
- parsing/formatting failures;
- class imbalance;
- OOD status;
- evidence amount.

Where feasible, perform leave-one-agent-out analysis to test whether the signal depends entirely on one weak or idiosyncratic agent.

If agent disagreement merely acts as a proxy for low confidence or one bad agent, narrow the claim accordingly.

## Phase 5 — Only if retrospective signal survives

Only after Phases 1–4 survive should the project consider a small prospective abstention policy.

Possible next experiment:

- freeze uncertainty features on a development set;
- define an abstention score;
- evaluate on unseen questions / entities / datasets;
- compare against confidence-only abstention.

Do not build a trainable router, multi-agent controller, or human-defer policy yet unless the cheap version clearly works.

## Decision criteria

### STRONG GO

Disagreement is reproducibly associated with error, provides incremental value beyond simple baselines, and improves selective prediction under a meaningful held-out split.

### GO

The effect is real and useful but one major robustness test remains.

### GO-NARROW

Reliability prediction works, but the useful signal is not broadly 'multi-agent disagreement' — e.g. only evidence conflict or one specific agent relationship matters.

### PIVOT

A related reliability question is supported, but the original disagreement framing is not.

### KILL

Disagreement does not meaningfully predict errors, does not beat simple baselines, or collapses under basic controls.

## Scope limits

Do not start with:

- learned abstention policies;
- new multi-agent architectures;
- model fine-tuning;
- prompt-search sweeps;
- huge benchmark construction;
- larger local models to rescue weak results.

The cheapest decisive retrospective analysis comes first.
