# Keep initial lab workloads disposable and recovery material outside the cluster

The Platform Lab prioritizes rebuilding and troubleshooting within a small time and spending budget. Initial applications, databases, and telemetry may be lost when the cluster is destroyed; source, infrastructure state, recovery credentials, and learning records must remain recoverable outside it. This accepts workload data loss to keep early experiments small and avoids depending on the failed cluster to rebuild it; persistent workload recovery requires a later, separate acceptance exercise.
