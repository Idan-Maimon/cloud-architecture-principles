# Check Catalogue

Every [quality goal](../quality-goals/README.md) scenario has **one check**. A check passes or fails,
and its level decides how serious a failure is. How levels and ranking work: [the scorecard guide](README.md).

| Level | Checks | A failed check is |
|---|---|---|
| **Bronze**: ready for production | 7 | **High risk** |
| **Silver**: operable and secure | 16 | **Medium risk** |
| **Gold**: resilient and portable | 8 | **Low risk** |

**Scope:** *Deployment* checks are evaluated on every deployment (cluster or site) separately.
*Service* checks are evaluated once for the whole service and apply to all its deployments.

**Signal:** where the result comes from. *(review)* means a person records the result in a
[scorecard review](review-guide.md); everything else is collected automatically. Where each automated
check is implemented (policy, pipeline template, alert rule) is recorded in the platform repositories,
not here.

Targets marked `N` come from the scenario's measure and are still to be calibrated.

## QG1 Security

| ID | Scenario | Check passes when… | Scope | Signal | Level |
|---|---|---|---|---|---|
| QG1.1 | Zero trust | Every endpoint requires authentication through the platform identity provider; nothing is trusted by network location | Deployment | Policy compliance | Bronze |
| QG1.2 | Encryption | Storage encryption and TLS 1.2+ are enabled | Deployment | Policy compliance | Bronze |
| QG1.3 | Audit | Audit logs are forwarded to the central log store with the declared retention | Deployment | Policy compliance | Silver |
| QG1.4 | Least privilege | No standing admin access outside break-glass accounts, and access was reviewed on schedule | Deployment | Policy compliance + access review record | Silver |
| QG1.5 | Secret handling | Secret scanning finds no secrets in the service's repositories or images | Service | CI pipeline | Bronze |

## QG2 Reliability

| ID | Scenario | Check passes when… | Scope | Signal | Level |
|---|---|---|---|---|---|
| QG2.1 | Availability | An approved SLO document and error budget policy exist ([SLA framework](https://github.com/Idan-Maimon/sla-framework), Step 3) | Service | SLO document in git | Bronze |
| QG2.2 | Failure containment | A zone or cell loss exercise in the last 12 months passed without breaching the SLO | Deployment | Exercise record *(review)* | Gold |
| QG2.3 | Component failure | A component failure test in the last quarter recovered within N minutes, with no data loss | Deployment | Test record *(review)* | Silver |
| QG2.4 | Recoverability | RPO and RTO are declared, and backups run on schedule within the RPO | Deployment | Backup tool | Silver |
| QG2.5 | Restore test | A restore test passed in the last quarter | Deployment | Backup tool | Silver |
| QG2.6 | Overload | A load test showed the service sheds or queues load, with admitted requests within SLO | Service | Load test record *(review)* | Gold |
| QG2.7 | Early warning | Alerts for certificate expiry and quorum loss fire at least N days/hours ahead | Deployment | Alert rules | Silver |

## QG3 Performance Efficiency

| ID | Scenario | Check passes when… | Scope | Signal | Level |
|---|---|---|---|---|---|
| QG3.1 | Data-plane latency | Data-plane latency is measured against a published target (SLO or benchmark) | Service | Metrics | Silver |
| QG3.2 | Lifecycle latency | The duration of each operation (R1–R4) is measured against a published target | Service | Metrics | Silver |
| QG3.3 | Capacity | Capacity limits are published, and alerts fire at N% of each limit | Deployment | Alert rules | Silver |
| QG3.4 | Noisy neighbour | A noisy-neighbour test kept other tenants' p99 within N% | Service | Load test record *(review)* | Gold |

## QG4 Operability

| ID | Scenario | Check passes when… | Scope | Signal | Level |
|---|---|---|---|---|---|
| QG4.1 | Everything as code | All configuration is synced from git, with no drift | Deployment | GitOps sync status | Silver |
| QG4.2 | Observability | SLO dashboards and burn-rate alerts are live (SLA framework, Step 4) | Deployment | Dashboards and alert rules | Silver |
| QG4.3 | Diagnosis | Every alert links to a runbook | Service | Alert rules | Silver |
| QG4.4 | Learning | Every major incident in the last quarter had a post-incident review within N days | Service | Ticketing system | Silver |

## QG5 Flexibility

| ID | Scenario | Check passes when… | Scope | Signal | Level |
|---|---|---|---|---|---|
| QG5.1 | Replace or exit a provider | Every provider the service depends on has an exit plan ADR, reviewed in the last N months | Service | ADRs in git | Gold |
| QG5.2 | Transferability | The service runs on at least two sites from the same repository and pipeline, with no manual steps | Service | CI/CD pipeline | Gold |

## QG6 Consumability

| ID | Scenario | Check passes when… | Scope | Signal | Level |
|---|---|---|---|---|---|
| QG6.1 | Self-service | R1–R4 are available through API, CLI or portal, and no routine-operation tickets were opened last quarter | Service | Ticketing system | Bronze |
| QG6.2 | Discoverability | The service is listed in the central catalogue with documentation, API reference, examples and SLO | Service | Service catalogue | Bronze |
| QG6.3 | Functional correctness | A published conformance suite passes before every release | Service | CI pipeline | Gold |
| QG6.4 | Time to first use | A new consumer, using only the documentation, gets a working instance within N minutes | Service | Test record *(review)* | Gold |
| QG6.5 | Error protection | Validation errors say how to fix the request | Service | API tests *(review)* | Silver |
| QG6.6 | Stable, standard interface | The API is versioned and documented (OpenAPI, AsyncAPI…), and CI blocks breaking changes outside a new version | Service | CI pipeline | Silver |

## QG7 Cost Efficiency

| ID | Scenario | Check passes when… | Scope | Signal | Level |
|---|---|---|---|---|---|
| QG7.1 | Attribution | Admission policy rejects resources without owner, cost-centre and environment labels | Deployment | Policy compliance | Bronze |
| QG7.2 | Opportunism | At least N% of unclaimed capacity is offered for opportunistic use | Deployment | Capacity metrics | Gold |
| QG7.3 | Cost visibility | A monthly report per service and department is published, with right-sizing recommendations | Service | Cost report | Silver |

## QG8 Sustainability

No checks while QG8 is a candidate for removal.
