# QG10 — Sustainability

**ISO/IEC 25010:2023:** not a product quality characteristic; related to Performance efficiency → Resource utilization
**Cloud frameworks:** AWS — Sustainability; Google Cloud — Sustainability

## Statement

Our energy and hardware footprint goes down as utilisation goes up. Every service is designed to deliver its outcome with the least energy, hardware and waste.

## Why it matters

- As owners of the data centres, we carry the full environmental impact of our cloud.
- Energy and hardware are a growing share of total cost.
- Sustainability reporting is increasingly a regulatory and corporate obligation.

## Quality Scenarios

| ID | Scenario | Stimulus | Expected response | Measure |
|---|---|---|---|---|
| QG10.1 | Utilisation | The fleet operates normally | Utilisation targets are met and reported | Compute utilisation ≥ N%; reported monthly |
| QG10.2 | Idle reclamation | A resource stays idle | It is detected and reclaimed automatically | Reclaimed after N days idle, with owner notice |
| QG10.3 | Hardware lifecycle | A hardware generation reaches review | Refresh is decided on energy efficiency as well as cost | Performance-per-watt included in every refresh decision |
| QG10.4 | Energy visibility | A service or department reviews its footprint | Energy use (or an agreed proxy) is visible | Reported per service and department |
| QG10.5 | Data lifecycle | Data passes its retention period | It is moved to colder storage or deleted | 100% of data under a lifecycle policy |

## Design Principles

1. **Maximise utilisation.** Consolidate workloads and pack them densely; idle hardware is waste.
2. **Reclaim what is unused.** Detect and remove idle resources, unused images and orphaned volumes automatically.
3. **Scale with demand.** Scale down as eagerly as scaling up.
4. **Manage the data lifecycle.** Keep only what is needed, on the most efficient storage tier.
5. **Choose efficient hardware.** Include performance-per-watt in procurement and refresh decisions.
6. **Make the footprint visible.** Report energy (or a proxy) so teams can act on it.

## Review Checklist

- Does the service scale down when demand drops?
- Are idle resources detected and reclaimed?
- Is there a lifecycle policy for all stored data?
- Is the service's energy or utilisation footprint reported?
- Was energy efficiency considered in hardware choices?

## Example

The platform consolidates under-used VMs onto fewer hosts overnight and powers down the freed servers, reclaims volumes orphaned for N days, moves logs older than N days to cold storage, and reports utilisation and estimated energy per department every month.
