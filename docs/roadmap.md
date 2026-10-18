# Learning roadmap

Milestone 1 is accepted for implementation planning; implementation and provisioning have not begun. Later milestones are outcome-oriented candidates; tools and detailed designs remain open. Each must fit the two-to-three-hour weekly time budget and S$30 monthly infrastructure ceiling or be simplified, shortened, or deferred.

| Phase | Useful outcome | Observable completion evidence | Human learning evidence |
| --- | --- | --- | --- |
| 1. Reproducible foundation | One private K3s node and a stateless workload, with a minimal Software Factory workflow | Reviewed change; credential-free checks; verified bootstrap and runtime; diagnosed failure; clean repeat plan; teardown and recreation; external recovery-copy test | Explain resource/state boundaries, control plane, runtime, basic scheduling and service path; perform diagnosis and rebuild without agent answers |
| 2. Controlled delivery | Reviewed desired state reaches the cluster through a deliberate delivery policy | Demonstrate reconciliation, drift detection and rollback; show exactly what approval authorizes deployment | Explain desired versus actual state, CI versus reconciliation, rollback versus destructive replacement; revisit ADR 0002 before introducing automatic delivery |
| 3. Operational diagnostics | Enough telemetry to answer a specific failure question | Trace a deliberately failed request or resource problem to supporting logs/metrics; measure stack resource use | Form hypotheses, select evidence and verify recovery; add traces only when a concrete question needs them |
| 4. Stateful recovery | A small stateful workload can survive the chosen failure scenario | Restore data from an independent backup and verify contents; measure recovery time and data loss | Explain storage lifecycle, backup versus replication, recovery-time and recovery-point objectives |
| 5. Agent runtime fundamentals | A reviewed agent application runs with explicit state, tool and resource boundaries | Demonstrate a bounded task, failure handling, state lifecycle and observable tool calls under a separately agreed API allowance | Explain runtime orchestration, persistence, tool execution and model/API failure behavior |
| 6. Agent authority and auditing | Tool permissions are enforced and unauthorized actions are observable | Attempt an allowed and a denied action; prove enforcement outside the model; correlate intent, identity, tool call and result; test credential/execution boundaries | Explain policy enforcement, least privilege, audit limitations and the difference between reviewed code and untrusted execution |
| 7. Agent-assisted maintenance | An agent proposes a safe platform maintenance change or incident remediation | Plan, change, deterministic checks, reviewable evidence and human-triggered runtime verification; compare with the initial workflow | Independently assess the proposal and explain remaining uncertainty before accepting it |

Stateful recovery can move earlier if it becomes a prerequisite for an agent-runtime experiment. Multi-node scheduling, kubeadm bootstrap and CNI replacement are separate targeted experiments, not mandatory additions to every phase. A Kubernetes Job alone is not acceptance evidence of isolation for hostile code.

## First six-week checkpoint

Review evidence rather than component count. Record elapsed sessions, actual spending, routine maintenance effort, successful and failed checks, and what the engineer can explain without agent answers. If the foundation runs but understanding or troubleshooting evidence is missing, continue phase 1. Do not install GitOps or another stack to manufacture visible progress.

Each weekly session should have one bounded learning objective, one observable result and a brief learning record, followed by resource cleanup or a recorded retention exception. Recovery and verification, once automated, must fit within one two-to-three-hour session, excluding provider outages and capacity shortages. This does not estimate total implementation effort.
