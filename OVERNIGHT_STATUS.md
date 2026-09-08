# Overnight Status

CURRENT CLAIM:

Multi-agent disagreement may provide incremental uncertainty information for biomedical drug reasoning, but this is currently untested.

STRONGEST EVIDENCE:

None yet. The project has only been initialized.

STRONGEST ALTERNATIVE EXPLANATION:

Any apparent disagreement signal may simply proxy low model confidence, question difficulty, evidence scarcity, one systematically weak agent, or OOD status.

FALSIFICATION ATTEMPT:

Not yet run. First priority is an identifiability/data audit followed by a cheap retrospective disagreement-vs-error test.

DECISION: GO

NEXT EXPERIMENT:

Audit available DrugAgent-style outputs and correctness labels; if identifiable, compare simple disagreement scores against confidence/vote/evidence baselines for error detection and selective prediction.

ESTIMATED COST:

Low if suitable outputs already exist inside the repository or can be reproduced cheaply; otherwise stop and document the blocker before expensive generation.
