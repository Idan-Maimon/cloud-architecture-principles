# QG3 — Performance Efficiency

**ISO/IEC 25010:2023:** Performance efficiency → Time behaviour, Resource utilization, Capacity (`#efficient`); Flexibility → Scalability
**Cloud frameworks:** AWS — Performance efficiency; Google Cloud — Performance optimization

## Statement

Every service delivers predictable, measured performance and is sized to demand. Performance targets are published, tested and monitored; capacity limits are known before they are reached.

## Why it matters

- Consumers can only design their systems if our latency and throughput are predictable.
- Unknown capacity limits turn growth into outages.
- Over-provisioning to hide unpredictability wastes money and energy (see QG9, QG10).

## Quality Scenarios

| ID | Scenario | Stimulus | Expected response | Measure |
|---|---|---|---|---|
| QG3.1 | Data-plane latency | Requests under normal load | Responses within published targets | p95 ≤ N ms; p99 ≤ N ms |
| QG3.2 | Lifecycle latency | A consumer runs R1–R4 (provision, modify, upgrade, decommission) | The operation completes in a deterministic time | p95 ≤ N minutes per operation |
| QG3.3 | Capacity | Usage approaches the service's declared limit | Owners are alerted before saturation | Alert at ≥ N% of limit; limits published |
| QG3.4 | Noisy neighbour | One tenant generates heavy load | Other tenants' performance stays within target | Other tenants' p99 unaffected beyond N% |

## Design Principles

1. **Publish performance targets.** Every service states latency, throughput and lifecycle-operation times as SLOs.
2. **Measure, don't guess.** Benchmark before release and monitor in production with the same metrics.
3. **Know your limits.** Every service publishes its tested capacity limits and alerts before they are reached.
4. **Isolate tenants.** Use quotas, limits and resource classes so one consumer cannot degrade another.
5. **Match resources to workload.** Offer resource classes (CPU, memory, storage tiers) and let consumers choose by need.

## Review Checklist

- Are latency, throughput and lifecycle-operation targets published?
- Have capacity limits been tested and published?
- Is there an alert before capacity is exhausted?
- Are tenants protected from noisy neighbours?

## Example

A Kubernetes-as-a-service offering publishes "cluster provisioned in ≤ N minutes at p95", enforces per-tenant quotas, and alerts the platform team when a site reaches N% of its node capacity.
