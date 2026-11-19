# QG7 — Cost Efficiency

**ISO/IEC 25010:2023:** Performance efficiency → Resource utilization (`#efficient`)
**Cloud frameworks:** AWS — Cost optimization; Google Cloud — Cost optimization

## Statement

Every unit of capacity is attributed to an owner, justified by business value and right-sized. Cost is visible to those who create it, and the organisation manages cloud spend as a capability.

## Why it matters

- In a private cloud the hardware is already paid for; waste shows up as unavailable capacity and early purchases.
- Without attribution, no department has a reason to optimise.
- Visible cost per unit of business output lets the organisation measure real return.

## Quality Scenarios

| ID | Scenario | Stimulus | Expected response | Measure |
|---|---|---|---|---|
| QG7.1 | Attribution | A resource is created | It carries owner, cost centre and environment tags | 100% tagged; untagged resources rejected |
| QG7.2 | Opportunism | A resource is allocated but not claimed by its owner | Other consumers can claim it, knowing the owner may take it back at any moment | ≥ N% of unclaimed capacity available for opportunistic use |
| QG7.3 | Cost visibility | A month closes | Each department sees its usage, its cost per unit of business output, and right-sizing recommendations | Report per service and per department every month; recommendations issued for resources below N% utilisation |

## Design Principles

These follow the AWS cost optimization design principles, adapted for a private cloud.

1. **Implement cloud financial management.** Cost is owned as a capability with dedicated people, processes and reporting.
2. **Adopt a consumption model.** Consumers use what they need and release what they do not; capacity follows demand.
3. **Measure overall efficiency.** Track business output against the cost of delivering it.
4. **Analyse and attribute expenditure.** Every resource is attributed to an owner; usage and cost are transparent.
5. **Make cost a design input.** Cost is reviewed alongside performance and reliability in every design.

## Review Checklist

- Is every resource tagged with owner, cost centre and environment?
- Does the service report utilisation and cost per unit of output?
- Is there a right-sizing process for over-provisioned resources?
- Does each department receive a monthly showback report?

## Example

Capacity a department has reserved but is not using is claimed by other teams for batch work, which give it back as soon as the owner needs it; every VM carries cost-centre tags; and the monthly showback report shows cost per transaction for their application, with right-sizing recommendations for idle databases.
