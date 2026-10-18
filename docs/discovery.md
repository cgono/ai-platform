# Discovery record

This document records the requirements interview. It is not an implementation specification; specifications belong in GitHub Issues for `cgono/ai-platform`.

## Confirmed in round 1

- Learning takes priority over automation. A working system and passing checks are insufficient without a Human Demonstration.
- The first phase prioritizes rebuilding and troubleshooting a small Kubernetes environment. An established coding agent and explicit workflow are the starting Software Factory; custom orchestration requires a demonstrated limitation.
- Plan around two to three hours per week. Four hours is a fallback offered by the engineer, not the default commitment.
- Initial lab applications, databases, and telemetry are disposable. Source, infrastructure state, recovery credentials, and learning records must remain recoverable outside the cluster.
- Initial workloads require human review. Autonomous tool execution and externally supplied code are deferred to a separate sandbox experiment.
- Agent governance, auditing, and prevention of unauthorized actions are important later learning objectives, including their relevance to the engineer's workplace.
- Initial infrastructure spending has a ceiling of S$30 per month, including retained resources and experiments. More expensive experiments must be shortened, simplified, or deferred. AI spending is tracked separately.

## Proposed planning interpretation

- Use six weeks as a review checkpoint rather than a completion promise. The first milestone's scope and timing remain to be agreed.

## Confirmed in round 2

- The first milestone targets one reproducible Kubernetes environment, one tiny workload, teardown and rebuild, and the engineer's explanation. GitOps, comprehensive observability, and agent runtimes are deferred.
- Two to three hours is the weekly time budget, not an estimate for the whole milestone. The milestone requires multiple sessions; its total duration has not been agreed.
- The engineer has some Linux service troubleshooting experience and uses external references, but does not consider this intermediate proficiency. Kubernetes knowledge is at beginner level. Infrastructure state knowledge currently covers its existence as a local or remotely stored file. Networking and container proficiency remain unassessed.
- Agents may help author automation. The engineer personally executes the first teardown, rebuild, and troubleshooting exercise using the runbook.
- The lab need not remain available between experiments. Resource retention versus destruction remains open pending provider economics and recovery requirements.
- The initial Software Factory must turn an agreed task into a reviewable change, run specified checks, and provide independently inspectable evidence. Autonomous planning loops and multiple agent roles are deferred.
- Use existing coding-agent access initially. No unattended API spending is authorized; a separate allowance must precede that capability.

## Unresolved

This list reflects the latest round, rather than the historical uncertainty at each earlier round.

- Final provider, region, available instance and verified all-in cost; Hetzner is preferred conditionally.
- A successful recovery test of the accepted 1Password and OneDrive arrangement before provisioning.
- Exact pinned software versions and implementation details, selected during implementation planning against the accepted specification.
- Paid API allowance and later agent runtime/governance designs, deferred beyond the first milestone.

## Confirmed in round 3

- Start with a self-managed cloud VM, including responsibility for the host, Kubernetes installation, and recovery.
- Geography is flexible; a distant region is acceptable for synthetic, latency-insensitive experiments. Workplace data and credentials are excluded unless a later use case is explicitly authorized.
- The engineer is comfortable with IP addresses, CIDR, ports, DNS, and routes to an extent; advanced routing protocols are not familiar. Container experience includes building images, local Docker execution, execution on services such as EKS, and log inspection. Storage experience includes Dockerfile volume declarations; runtime mounts and persistence semantics should be checked through exercises.
- Merging a change does not authorize applying it. Provisioning, modification, and destruction require a separate human-triggered step showing the intended action and target environment.
- Reproducibility must cover complete loss of the VM, using the repository and an inventoried recovery kit. Every manual prerequisite must be documented. Credentials and infrastructure state belong outside the repository. A recovery-time target remains open.

## Confirmed in round 4

- Start with K3s. Its packaging must not replace understanding: the engineer must identify the control-plane components, datastore, runtime, and networking responsibilities. kubeadm bootstrap can be a later comparative exercise.
- Hetzner is a candidate, not a dependency. Consider similarly affordable alternatives. A suitable available instance and total cost, including tax, network resources, and currency conversion, must fit the budget before provisioning.
- The first workload requires no public endpoint, domain, or ingress. Administration and workload access are restricted to the engineer through an authenticated path.
- Completion requires explaining the path from workload declaration to running container and reachable service; diagnosing an introduced workload failure using status, events, and logs; and recreating the VM and workload from the repository and Recovery Kit.
- The initial workload is stateless. Persistent workload recovery remains a separate later exercise.

## Confirmed in round 5

- Use OpenTofu for cloud resources and cloud-init for initial host bootstrapping. Add Ansible only for a demonstrated configuration-management need. VM creation and successful bootstrap require separate evidence.
- Start with encrypted local OpenTofu state on the engineer's workstation and a recoverable backup outside the lab. The actual backup and key-storage arrangement remains unresolved.
- Use key-authenticated SSH for initial administration, Kubernetes commands on the node, and tunnels for workload access where needed. The Kubernetes API must not be publicly exposed; firewall restrictions require explicit configuration.
- Coding agents author changes and run checks without supplied live cloud or cluster credentials. The engineer executes authenticated provisioning and runtime verification. The implementation must identify technical enforcement versus supervised workflow restrictions, including ambient credential exposure on a shared workstation.
- Pre-apply evidence covers formatting, configuration validation, bootstrap checks, and human review of intended infrastructure changes. Post-apply evidence covers bootstrap completion, Kubernetes health, workload reachability, failure diagnosis, an infrastructure plan without unintended changes, and teardown/recreation.

## Architecture clarification

- The initial deployment rents a Linux VM from the selected cloud provider and installs K3s on it. The VM is a single Kubernetes node hosting both control-plane components and workloads; this is self-managed Kubernetes, not a managed Kubernetes service.

## Confirmed in round 6

- Prefer short commitments and disposable hourly resources over the cheapest subscription headline. Hetzner remains preferred conditionally; alternatives may be considered without raising the spending ceiling.
- Destroy lab resources at session end by default, including billable supporting resources. Preserving an unfinished experiment requires an explicit exception within budget.
- Recovery backups must be encrypted, outside Git and outside the lab, with decryption material stored separately. The engineer has 1Password, OneDrive, and iCloud; their proposed use is under review, not yet a confirmed implementation choice.
- Use GitHub Actions for credential-free pull-request checks and local human execution for authenticated operations. The engineer confirms the repository is public.
- Once automation is established, rebuilding and verification must fit within one two-to-three-hour session, excluding provider outages and unavailable capacity. This is not an implementation-duration estimate.
- At the six-week checkpoint, continue the first milestone if understanding or troubleshooting evidence is insufficient; do not add components merely because the platform runs.

## Consolidated draft

The first-milestone specification is [GitHub issue #1](https://github.com/cgono/ai-platform/issues/1). The vision, architecture and roadmap documents summarize the interview; the issue is the canonical specification. No implementation or provisioning has begun.

## Specification review accepted — 2026-10-18

- The engineer confirmed shared understanding and accepted the consolidated milestone 1 scope and design, including 1Password for the state-encryption passphrase and OneDrive for dated encrypted state backups.
- Provider selection remains conditional on suitable available capacity and verified all-in cost within the existing budget.
- Acceptance does not authorize implementation or provisioning. Recovery testing and implementation planning remain future work.
- Backup retention, identification of the latest completed backup, and the exact fault exercise belong in implementation planning. A fault may produce no container logs; its evidence must explain the observed behavior rather than require nonexistent logs.
- No further milestone-level discovery questions remain. The engineer subsequently confirmed issue #1 is suitable to proceed to implementation planning. Its accepted status and reasonable design-review corrections are synchronized to the canonical issue; implementation and provisioning remain unauthorized.
