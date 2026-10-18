# Vision and scope

Build a small, reproducible Platform Lab that makes its engineer more capable of explaining, evaluating, troubleshooting, and recovering cloud-native systems while using AI to assist engineering work.

Platform engineering is the primary objective. The Software Factory is initially an established coding agent plus an explicit specification, review, validation, and evidence workflow. Custom orchestration must address an observed limitation before becoming a project of its own.

## Constraints

- Two to three hours of engineering time per week. Six weeks is a review checkpoint, not a delivery promise.
- Infrastructure spending must remain within S$30 per month, including tax, currency conversion, retained resources, and experiments. Existing coding-agent access is the initial AI budget; unattended paid API use is deferred.
- Initial workloads use synthetic data and are disposable. Household infrastructure and workplace data and credentials are outside the lab.
- Source, infrastructure state, recovery credentials, and learning records remain recoverable outside the cluster.
- Human review is required for initial workloads. Merging code does not authorize live changes; the engineer separately triggers provisioning, modification, and destruction.

## First useful outcome

An agent helps produce reviewed infrastructure and bootstrap configuration for one self-managed cloud VM running K3s and a tiny stateless workload. Credential-free checks run on pull requests. The engineer provisions it, explains it, diagnoses an introduced failure, and recreates it from the repository and Recovery Kit.

Completion requires both observable system behavior and a Human Demonstration. Documentation and external references are permitted during demonstrations; an agent must not provide the diagnosis or recovery steps during the assessment. Passing automated checks alone is insufficient.

## Deferred capabilities

Multi-node and highly available clusters; persistent application recovery; GitOps; public application endpoints; a full telemetry stack; Cilium; Ansible without a demonstrated need; custom agent orchestration; autonomous remediation; and execution of externally supplied or unreviewed code.

Agent runtime fundamentals, authority controls, auditing, and prevention of unauthorized actions are important later objectives. Governance of agents building the platform and governance of agents running on it are separate experiments.

## How to judge progress

- Can the engineer explain each component's purpose, interactions, alternatives, and failure modes?
- Can the engineer recover the lab and diagnose a workload failure using evidence?
- Are changes traceable from agreed requirements through review and validation?
- Does the lab fit its spending and time constraints, including maintenance effort?
- Does an added component solve a demonstrated problem or teach a specific capability?

Canonical terminology is in the root glossary; architectural trade-offs are in `docs/adr/`. Specifications live in GitHub Issues, and this document does not replace them.
