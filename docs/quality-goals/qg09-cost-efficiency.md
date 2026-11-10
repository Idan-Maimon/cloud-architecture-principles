# QG9 — Cost Efficiency

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
| QG9.1 | Attribution | A resource is created | It carries owner, cost centre and environment tags | 100% tagged; untagged resources rejected |
| QG9.2 | Consumption model | Non-production environments outside working hours | They scale to zero or are scheduled off | ≥ N% reduction in non-production off-hours usage |
| QG9.3 | Efficiency | A service reports its consumption | Utilisation and cost per unit of business output are visible | Reported monthly per service and per department |
| QG9.4 | Right-sizing | A resource is over-provisioned | The owner receives a right-sizing recommendation | Recommendations issued for resources below N% utilisation |
| QG9.5 | Showback | A month closes | Each department sees its usage and cost | Showback report per department every month |
| QG9.6 | Build vs reuse | A team plans to build its own infrastructure capability | It uses the platform service unless an ADR justifies otherwise | 0 unjustified duplicate capabilities |

## Design Principles

These follow the AWS cost optimization design principles, adapted for a private cloud.

1. **Implement cloud financial management.** Cost is owned as a capability with dedicated people, processes and reporting.
2. **Adopt a consumption model.** Consumers use what they need and release what they do not; capacity follows demand.
3. **Measure overall efficiency.** Track business output against the cost of delivering it.
4. **Stop undifferentiated heavy lifting.** Use platform services instead of building and running your own.
5. **Analyse and attribute expenditure.** Every resource is attributed to an owner; usage and cost are transparent.
6. **Make cost a design input.** Cost is reviewed alongside performance and reliability in every design.

## Review Checklist

- Is every resource tagged with owner, cost centre and environment?
- Do non-production environments scale down outside working hours?
- Does the service report utilisation and cost per unit of output?
- Is there a right-sizing process for over-provisioned resources?
- Is the team using platform services where they exist?
- Does each department receive a monthly showback report?

## Example

A department's development clusters scale to zero every evening and weekend, every VM carries cost-centre tags, and the monthly showback report shows cost per transaction for their application, with right-sizing recommendations for idle databases.
