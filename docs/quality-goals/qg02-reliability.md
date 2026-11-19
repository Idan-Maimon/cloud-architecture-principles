# QG2 — Reliability

**ISO/IEC 25010:2023:** Reliability → Faultlessness, Availability, Fault tolerance, Recoverability; Safety → Fail-safe behaviour, Hazard warning (`#reliable`, `#safe`)
**Cloud frameworks:** AWS — Reliability; Google Cloud — Reliability

## Statement

Every service publishes its service level objective (SLO) and keeps it through the failure of any single component or zone. Failures are expected and designed for; recovery is automatic and tested.

## Why it matters

- Consumers build their own commitments on top of ours; an unstated SLO cannot be relied on.
- In a shared private cloud, one service's outage cascades into many departments.
- Untested recovery is not recovery.

## Quality Scenarios

| ID | Scenario | Stimulus | Expected response | Measure |
|---|---|---|---|---|
| QG2.1 | Availability | Normal operation over a rolling 4-week window | Each operation (R1–R4) and the running instance meet their SLOs | SLOs set per operation from measured data, following the [SLA framework](https://github.com/Idan-Maimon/sla-framework); error budget policy agreed (see [Requirements and qualities](../principles/requirements-and-qualities.md)) |
| QG2.2 | Failure containment | A zone is lost, or a failure or bad change hits one tenant, cell or zone | Impact stays inside that failure domain; Tier 1 and Tier 2 services keep serving | SLO not breached; no manual intervention; 0 incidents spanning more than one failure domain |
| QG2.3 | Component failure | A single instance, node, disk or dependency fails | Traffic moves to healthy instances automatically, or the service degrades in a controlled way | Recovery ≤ N minutes; no data loss or corruption |
| QG2.4 | Recoverability | Data is lost, corrupted or deleted by mistake | The service is restored from backup, or recovered within the protection window | Within the declared RPO and RTO; deleted instances and data recoverable for ≥ N days |
| QG2.5 | Restore test | Scheduled recovery exercise | Restore succeeds end to end | Tested at least quarterly; results recorded |
| QG2.6 | Overload | Demand exceeds capacity | The service sheds or queues load instead of failing | Error rate stays within SLO for admitted requests |
| QG2.7 | Early warning | A risky condition develops (certificate expiry, quorum loss) | Owners are warned before impact | Warning ≥ N days/hours ahead |

## Design Principles

1. **SLOs per operation, tiers for architecture.** SLO targets are set per operation from measured data. A service's tier sets only its architecture: zone spread, RPO, RTO and review frequency.
2. **No single point of failure.** Tier 1 and Tier 2 services run across at least three zones (or N failure domains).
3. **Automate recovery.** Health checks, self-healing and failover are automatic; humans handle what automation cannot.
4. **Back up and prove it.** Every stateful service has automated backups and a scheduled, recorded restore test. Destruction is reversible: soft-delete, protection periods and deletion locks on critical resources.
5. **Degrade gracefully.** Use timeouts, retries with back-off, circuit breakers and load shedding. On uncertainty, stop and protect data rather than continue.
6. **Manage with error budgets.** When a service exhausts its error budget, reliability work takes priority over features.
7. **Test failure.** Chaos and failover exercises run regularly in production-like environments.
8. **Limit the blast radius.** Partition by tenant, cell and zone; changes and failures stay inside one partition.
9. **Warn before harm.** Detect and alert on conditions that will lead to incidents.

## Review Checklist

- Does every operation (R1–R4) and the running instance have an SLO and an error budget policy?
- Has the service declared its tier, RPO and RTO?
- Does it survive the loss of a zone without breaching its SLO?
- Is recovery automatic for single-component failures?
- When was the last successful restore test?
- Are timeouts, retries and circuit breakers in place for every dependency?
- Is an error budget tracked and acted on?
- What happens to data when each dependency fails?
- What is the largest possible blast radius of a failure or a bad change?
- Can deleted instances and data be recovered within the protection window?

## Example

An object storage service declares Tier 1: it replicates data across three zones, loses no writes when a zone fails, publishes SLOs for bucket creation and object reads, set from measured data, with an error budget dashboard, and restores a sampled bucket from backup every quarter.
