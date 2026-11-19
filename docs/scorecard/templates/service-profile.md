# Service Profile — `<Service name>`

> One per service, stored in the service's own repository next to its SLO document.
> Replace everything in `<…>`. How it is used: [the scorecard guide](../README.md).

| | |
|---|---|
| **Service owner** | `<name / team>` |
| **On-call** | `<rotation name>` |
| **Version** | 1.0 |
| **Last review** | `<date>` |
| **Next review** | `<date: yearly, or after a major change>` |

## Service overview

`<2–3 sentences: what the service does and for whom.>`

## Requirements offered

| ID | Requirement | Offered? | Through |
|---|---|---|---|
| R1 | Provision | `<yes / no>` | `<API, CLI, portal>` |
| R2 | Modify | | |
| R3 | Upgrade | | |
| R4 | Decommission | | |
| R5 | Use | | `<e.g. Kubernetes API, S3 endpoint>` |

## Deployments

Every place the service runs. Production deployments decide the service's level.

| Deployment | Site | Environment | Production? |
|---|---|---|---|
| `<site-a/cluster-01>` | `<site-a>` | `<prod>` | `<yes>` |

## Links

| Document | Link |
|---|---|
| SLO document and error budget policy | `<link>` |
| Architecture documentation (arc42) | `<link>` |
| Repository | `<link>` |
| Catalogue entry | `<link>` |

## Not applicable

Checks that don't apply to this service. They count as passed.

| Check | Reason | Approved by |
|---|---|---|
| `<QG2.4>` | `<stateless service: no data to back up>` | `<section leader>` |

## Exceptions

Failed checks accepted for now. Each one is an [exception ADR](exception.md) with an expiry date.

| Check | Deployment | Exception | Expires |
|---|---|---|---|
| `<QG7.2>` | `<all>` | `<link to ADR>` | `<date>` |

## Review results

Results of the checks marked *(review)* in the [catalogue](../check-catalogue.md), from the last
[scorecard review](../review-guide.md).

| Check | Deployment | Result | Evidence | Date |
|---|---|---|---|---|
| QG2.2 Failure containment | `<site-a/cluster-01>` | `<pass / fail>` | `<link>` | |
| QG2.3 Component failure | | | | |
| QG2.6 Overload | `<service>` | | | |
| QG3.4 Noisy neighbour | `<service>` | | | |
| QG6.4 Time to first use | `<service>` | | | |
| QG6.5 Error protection | `<service>` | | | |
