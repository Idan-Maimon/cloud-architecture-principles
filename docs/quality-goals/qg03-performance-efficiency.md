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
| QG3.4 | Scale out | Demand increases | The service adds capacity without downtime | Scale-out ≤ N minutes; 0 downtime |
| QG3.5 | Noisy neighbour | One tenant generates heavy load | Other tenants' performance stays within target | Other tenants' p99 unaffected beyond N% |
| QG3.6 | Performance regression | A new version is released | Performance is compared with the previous version | Release blocked on regression > N% |

## Design Principles

1. **Publish performance targets.** Every service states latency, throughput and lifecycle-operation times as SLOs.
2. **Measure, don't guess.** Benchmark before release and monitor in production with the same metrics.
3. **Know your limits.** Every service publishes its tested capacity limits and alerts before they are reached.
4. **Scale horizontally.** Prefer adding instances to growing them; design for scale-out from the start.
5. **Isolate tenants.** Use quotas, limits and resource classes so one consumer cannot degrade another.
6. **Match resources to workload.** Offer resource classes (CPU, memory, storage tiers) and let consumers choose by need.
7. **Test performance continuously.** Performance tests run in the pipeline and block regressions.

## Review Checklist

- Are latency, throughput and lifecycle-operation targets published?
- Have capacity limits been tested and published?
- Is there an alert before capacity is exhausted?
- Can the service scale out without downtime?
- Are tenants protected from noisy neighbours?
- Does the pipeline detect performance regressions?

## Example

A Kubernetes-as-a-service offering publishes "cluster provisioned in ≤ N minutes at p95", benchmarks every release against the previous one, enforces per-tenant quotas, and alerts the platform team when a site reaches N% of its node capacity.
