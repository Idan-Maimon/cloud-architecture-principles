# QG2 — Reliability

**ISO/IEC 25010:2023:** Reliability → Faultlessness, Availability, Fault tolerance, Recoverability (`#reliable`)
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
| QG2.2 | Zone failure | One availability zone is lost | Tier 1 and Tier 2 services keep serving | SLO not breached; no manual intervention |
| QG2.3 | Component failure | A single instance, node or disk fails | Traffic moves to healthy instances automatically | Recovery ≤ N minutes; no data loss |
| QG2.4 | Recoverability | Data is lost or corrupted | The service is restored from backup | Within the declared RPO and RTO |
| QG2.5 | Restore test | Scheduled recovery exercise | Restore succeeds end to end | Tested at least quarterly; results recorded |
| QG2.6 | Overload | Demand exceeds capacity | The service sheds or queues load instead of failing | Error rate stays within SLO for admitted requests |

## Design Principles

1. **SLOs per operation, tiers for architecture.** SLO targets are set per operation from measured data. A service's tier sets only its architecture: zone spread, RPO, RTO and review frequency.
2. **No single point of failure.** Tier 1 and Tier 2 services run across at least three zones (or N failure domains).
3. **Automate recovery.** Health checks, self-healing and failover are automatic; humans handle what automation cannot.
4. **Back up and prove it.** Every stateful service has automated backups and a scheduled, recorded restore test.
5. **Degrade gracefully.** Use timeouts, retries with back-off, circuit breakers and load shedding.
6. **Manage with error budgets.** When a service exhausts its error budget, reliability work takes priority over features.
7. **Test failure.** Chaos and failover exercises run regularly in production-like environments.

## Review Checklist

- Does every operation (R1–R4) and the running instance have an SLO and an error budget policy?
- Has the service declared its tier, RPO and RTO?
- Does it survive the loss of a zone without breaching its SLO?
- Is recovery automatic for single-component failures?
- When was the last successful restore test?
- Are timeouts, retries and circuit breakers in place for every dependency?
- Is an error budget tracked and acted on?

## Example

An object storage service declares Tier 1: it replicates data across three zones, loses no writes when a zone fails, publishes SLOs for bucket creation and object reads, set from measured data, with an error budget dashboard, and restores a sampled bucket from backup every quarter.
