# Service Profile — Hosted OpenShift Clusters on KubeVirt

> **Illustrative example.** Filled in from the [template](../../templates/service-profile.md).

| | |
|---|---|
| **Service owner** | Platform team lead |
| **On-call** | Platform on-call rotation |
| **Version** | 1.0 |
| **Last review** | 2026-11-19 |
| **Next review** | 2027-11-19, or after a major change |

## Service overview

Tenant teams get dedicated OpenShift clusters whose control planes run as hosted control planes on a
shared management cluster, and whose workers are KubeVirt virtual machines. The platform team
provisions, scales, upgrades and removes them.

## Requirements offered

| ID | Requirement | Offered? | Through |
|---|---|---|---|
| R1 | Provision | yes | Self-service workflow (API and portal) |
| R2 | Modify | yes | Self-service workflow: scale worker pools |
| R3 | Upgrade | yes | Platform-run upgrades, scheduled with the tenant |
| R4 | Decommission | yes | Self-service workflow |
| R5 | Use | yes | The hosted cluster's Kubernetes API and its workloads |

## Deployments

| Deployment | Site | Environment | Production? |
|---|---|---|---|
| site-a | site-a | prod | yes |
| site-b | site-b | prod | yes |
| site-c | site-c | prod | yes |

## Links

| Document | Link |
|---|---|
| SLO document and error budget policy | [SLA framework example](https://github.com/Idan-Maimon/sla-framework/tree/main/examples/hcp-kubevirt-platform) |
| Architecture documentation (arc42) | *(internal)* |
| Repository | *(internal)* |
| Catalogue entry | *(internal)* |

## Not applicable

| Check | Reason | Approved by |
|---|---|---|
| — | All checks apply | |

## Exceptions

| Check | Deployment | Exception | Expires |
|---|---|---|---|
| QG7.2 Opportunism | all | ADR: the platform scheduler can't yet give capacity back to its owner on demand | 2027-03-31 |

## Review results

| Check | Deployment | Result | Evidence | Date |
|---|---|---|---|---|
| QG2.2 Failure containment | site-a | pass | Zone-loss exercise record | 2026-09-14 |
| QG2.2 Failure containment | site-b, site-c | fail | No exercise yet | 2026-11-19 |
| QG2.3 Component failure | all | pass | Node and worker VM failure tests | 2026-10-02 |
| QG2.6 Overload | service | fail | No load test yet | 2026-11-19 |
| QG3.4 Noisy neighbour | service | fail | No test yet | 2026-11-19 |
| QG6.4 Time to first use | service | fail | Not measured | 2026-11-19 |
| QG6.5 Error protection | service | pass | Workflow validation messages reviewed | 2026-11-19 |
