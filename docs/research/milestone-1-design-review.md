# Milestone 1 design review — 2026-10-18

Claude Code independently reviewed the local discovery documents, glossary, ADRs, roadmap, recovery research and GitHub issue #1. The review was supplied as text with tools disabled. No implementation or provisioning was performed.

## Assessment and disposition

- F1 accepted as an acceptance-wording defect, rather than an architectural blocker. Invalid image pulls can prevent container startup, so the criterion now requires available logs and an explanation when none exist. Verified against [Kubernetes image documentation](https://kubernetes.io/docs/concepts/containers/images/).
- F2 accepted. Synchronize issue #1 and local summaries with the engineer's accepted scope and 1Password/OneDrive choice. Mark the issue ready for implementation planning only; live actions and implementation remain unauthorized.
- F3 partially accepted. Clarify that the planned teardown/recreation demonstration retrieves the post-destroy state backup from OneDrive and reconciles it against provider inventory before planning. Document unplanned-loss/stale-state reconciliation, without requiring another injected disaster exercise. The existing separate actual-state download/decryption gate remains required; the clean-destroy rebuild is not claimed as proof of stale-state recovery.
- F4 retained as implementation-planning details: passphrase retrieval path, reviewed revision verification, backup naming/retention/completion. Do not add a whole-account/workstation disaster-recovery test or require an Emergency Kit exercise; those are beyond the accepted failure boundary.

No architecture change or new ADR is warranted. Provider, capacity, cost, software versions and exact execution checks remain planning/preflight choices. No unresolved blocker remains in this design review; this is not implementation validation.

## Original Claude review

# Review: Milestone 1 specification

**Verdict:** One blocking specification defect (F1). F2 is a status inconsistency to fix before implementation planning starts. F3 and F4 are small clarifications. I found no problems with the budget, security boundary or provider conditionality that need reopening.

## Blocking

**F1. High: fault-diagnosis criterion requires logs that an invalid image cannot produce**
- **Where:** Issue #1, Acceptance evidence, fault bullet ("diagnosed with status, events and logs"). `docs/discovery.md` (acceptance record) says evidence must explain missing logs rather than require them.
- **Failure:** The engineer injects a bad image reference, as the issue suggests. The pod goes to `ErrImagePull`/`ImagePullBackOff`, no container ever starts, and `kubectl logs` returns an error. The checkbox cannot be satisfied literally. Alternatively, the engineer or an agent decides the demonstration fails, or substitutes unrelated logs to tick the box.
- **Correction:** Reword the bullet. Status and events are mandatory. Container logs are required only if a container started. If none exists, the evidence is the `kubectl describe`/events output plus a note that no container logs exist and why. Optionally require the implementation plan to name which fault is injected and which evidence it should yield.
- **Fit:** It is a one-line wording change that aligns the issue with the already-accepted discovery record. It adds no scope.

## Fix before implementation planning (not technical blockers)

**F2. Medium: the canonical spec still reads as an unaccepted draft**
- **Where:** Issue #1 ("Status: draft", "Proposed recovery arrangement — requires review", "Implementation planning inputs: accept the recovery-service choice", `needs-info` label). Also `README.md` ("Draft milestone 1 specification") and `docs/architecture.md` ("defines the acceptance gates for review").
- **Failure:** Discovery calls the issue canonical, and the agent workflow tracks specs in issues. An agent or a later reader following the issue concludes the recovery choice is still open. They either re-ask settled questions or treat the planning inputs as unmet.
- **Correction:** Have the human update the issue. Set status to accepted 2026-10-18, retitle the recovery section "Accepted", delete the "accept the recovery-service choice" input, and relabel. State explicitly that acceptance does not authorize implementation or provisioning. Update the README link text. I have not edited the issue, since that is outward-facing and you did not ask for it.
- **Fit:** It removes a contradiction and adds no new content.

**F3. Medium: "recreate from repository and Recovery Kit" doesn't say which state is restored**
- **Where:** Issue #1, destroy bullet ("retain and back up the resulting state") versus the recreate bullet ("Starting without the old VM…"). Also `architecture.md` ("complete VM loss… never restore old state blindly").
- **Failure:** The engineer destroys cleanly, so state is empty. Recreation then trivially succeeds and never exercises downloading a OneDrive copy, decrypting it and reconciling it against reality. Alternatively, they restore a pre-destroy backup, and the plan tries to manage VMs that no longer exist. Either way, the recovery evidence is weaker than the stated goal.
- **Correction:** Add one sentence to the recreate bullet. Recreation begins from the downloaded and decrypted OneDrive copy of the post-destroy state. The engineer records the reconcile check (state versus provider inventory) and the plan output before apply. Also state whether complete VM loss without a prior destroy is exercised or only documented.
- **Fit:** It clarifies an existing gate and adds no new mechanism.

## Planning details (not spec defects)

**F4. Low: recovery-test realism and change integrity, to settle in the implementation plan**
- **Passphrase retrieval:** The recovery test can pass using an already unlocked 1Password session. Make the plan retrieve the passphrase through the documented sign-in path, with the Emergency Kit location listed in the Recovery Kit inventory. The issue's inventory mentions "decryption access" but not how 1Password itself is reached. Whole-account loss stays out of scope.
- **Review-to-apply integrity:** "Code must not change unnoticed between review and execution" has no mechanism yet. The plan should say how to prevent drift, for example applying from a clean checkout of the merged commit and recording its SHA in the evidence.
- **Backup identification and retention:** These are already correctly deferred to planning. The plan should define a naming scheme and a "backup is complete" check, which covers the "latest completed backup" requirement.

## Checked, no defect found
- **Budget:** Hourly billing, destroy-by-default, inventory-verified cleanup, all-in accounting including FX and tax, and conditionality on capacity are consistent across the documents. Alerts are not claimed as hard caps.
- **Security boundary:** The public repo, credential-free CI, no agent credentials, and the supervised-versus-enforced distinction are consistent. The network-test limitation is already required to be documented.
- **Time and learning outcome:** Hours per week are treated as a budget rather than an estimate, and the Human Demonstration is a gating criterion. I found no contradiction.
- **Recovery mechanism:** Dated copies, the separate key, the non-live pre-provisioning test and the post-provisioning repeat are coherent.
