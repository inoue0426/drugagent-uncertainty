# DrugAgent Uncertainty

Falsification-first study of uncertainty estimation and selective abstention for multi-agent biomedical drug reasoning.

## Core question

Can disagreement among heterogeneous reasoning agents predict DrugAgent errors and support calibrated abstention beyond simpler uncertainty baselines?

The initial target is deliberately narrow:

> Does agent disagreement provide incremental error-detection value beyond confidence, majority vote, evidence amount/quality, or obvious OOD signals?

If not, stop. Do not rescue the idea with architecture complexity.

## First scientific gate

Retrospectively analyze existing or reproducibly generated DrugAgent-style outputs and compare:

1. single-model / aggregate confidence;
2. majority-vote margin;
3. inter-agent disagreement;
4. evidence-consistency / evidence-quality signals where available;
5. simple OOD / coverage baselines.

Primary outcomes:

- error detection (AUROC/AUPRC);
- calibration;
- selective risk;
- risk-coverage curves;
- retained accuracy as low-trust cases are rejected.

The key claim only survives if disagreement adds useful signal beyond simple baselines under leakage-safe evaluation.

## Research principles

- Falsify before optimizing.
- Prefer retrospective analyses over new model training.
- Never interpret multi-agent diversity itself as useful unless it predicts failures.
- Do not tune prompts or agent count merely to manufacture disagreement.
- Compare against embarrassingly simple baselines first.
- Report negative results and confounds explicitly.
- Stop when the central claim receives a clear GO / GO-NARROW / PIVOT / KILL decision.

## Local model

The current intended local inference backend is Ollama with `qwen3:30b` when generation is needed. The project should not assume that model scale is the source of the scientific contribution.

## Repository workflow

- `AGENTS.md` — autonomous-agent operating rules
- `RESEARCH_PLAN.md` — falsification gates
- `EXPERIMENT_LOG.md` — append-only experiment record
- `OVERNIGHT_STATUS.md` — current claim and next experiment
- `scripts/` — reproducible analyses
- `src/` — reusable project code
- `data/` — project-local data only
- `results/` — quantitative outputs and reports

## Decision standard

A positive result requires more than correlation between disagreement and error. The strongest version is:

> Agent disagreement predicts errors prospectively, adds information beyond simple confidence/evidence baselines, and produces a reproducible selective-prediction benefit.

Otherwise the project should narrow, pivot, or stop.
