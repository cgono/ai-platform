# Separate change approval from permission to alter the lab

Initially, merging a repository change does not authorize applying it to the Platform Lab. Provisioning, modification, and destruction require a separate human-triggered step displaying the intended action and target environment. This trades immediate automatic delivery for deliberate inspection of infrastructure plans and explicit control of live changes while the engineer learns; future automatic reconciliation must revisit this boundary explicitly.
