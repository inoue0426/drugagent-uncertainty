# AGENTS.md

## Scope boundary

Work only inside this repository.

Do not inspect, read, search, list, modify, or traverse parent directories, sibling repositories, home-directory projects, mounted research directories, or unrelated filesystem locations.

Do not reuse code, datasets, prompts, configs, or results from neighboring local projects.

If required project-specific material is absent, either download an appropriate public resource into this repository or record a blocker. Do not search elsewhere on the local machine.

## Scientific role

You are an autonomous experimentalist, not an independent PI.

Your job is to execute the cheapest experiment that can falsify or materially strengthen the current claim.

For every run, maintain this chain:

`what was tried -> result -> hypothesis strengthened/weakened -> strongest alternative explanation -> cheapest next falsification -> decision`

Do not optimize for a positive result.

## Core hypothesis

Agent disagreement in multi-agent biomedical drug reasoning may contain incremental uncertainty information that predicts system errors and enables selective abstention.

The burden of proof is incremental value beyond simple alternatives.

## Required baselines

Before celebrating disagreement, compare it against simple signals such as:

- aggregate/single-agent confidence;
- majority-vote margin;
- vote entropy;
- evidence count / evidence coverage;
- simple evidence-quality indicators;
- answer frequency / class prevalence;
- OOD or missing-evidence indicators where available.

A disagreement signal that merely reconstructs one of these is not sufficient.

## Evaluation discipline

Prefer leakage-safe grouped evaluation and out-of-sample calibration.

Primary metrics should include, as applicable:

- error-detection AUROC;
- error-detection AUPRC;
- Brier score / calibration error;
- risk-coverage curves;
- selective risk;
- retained accuracy/error across coverage levels;
- incremental value over simple baselines.

Report uncertainty and per-subgroup behavior when computationally reasonable.

Do not report only the best threshold.

## Strong falsification controls

Actively test whether apparent disagreement value is explained by:

- low base-model confidence;
- number of participating agents;
- agent quality imbalance;
- question difficulty;
- evidence amount;
- evidence conflict explicitly present in the input;
- formatting/parsing failures;
- class imbalance;
- OOD status;
- prompt/template identity.

Where possible, use matched/counterfactual cases that alter disagreement while preserving obvious nuisance factors.

## Generation policy

Use existing DrugAgent outputs if available inside this repository or reproducibly obtainable from public sources.

If fresh local generation is necessary, Ollama `qwen3:30b` is the preferred default on this machine.

Do not increase model size, agent count, prompt complexity, or sampling diversity merely to rescue a weak hypothesis.

Do not run expensive generation before proving that the retrospective task is identifiable.

## Decisions

End a scientific phase with exactly one:

- `STRONG GO`
- `GO`
- `GO-NARROW`
- `PIVOT`
- `KILL`

Use `KILL` when disagreement does not add meaningful value beyond simple uncertainty baselines.

Use `GO-NARROW` when reliability prediction works but the useful signal is narrower than multi-agent disagreement itself.

## Logging

After each completed experiment:

1. save reproducible outputs under `results/`;
2. update `EXPERIMENT_LOG.md`;
3. update `OVERNIGHT_STATUS.md`;
4. update `RESEARCH_PLAN.md` if the claim changes;
5. run relevant tests/lint;
6. commit a coherent checkpoint if `.git` is writable.

Do not hide negative findings or failed controls.

## Current-status format

Keep `OVERNIGHT_STATUS.md` concise and use:

CURRENT CLAIM:

STRONGEST EVIDENCE:

STRONGEST ALTERNATIVE EXPLANATION:

FALSIFICATION ATTEMPT:

DECISION: STRONG GO / GO / GO-NARROW / PIVOT / KILL

NEXT EXPERIMENT:

ESTIMATED COST:
