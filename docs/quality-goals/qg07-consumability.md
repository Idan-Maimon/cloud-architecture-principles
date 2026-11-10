# QG7 — Consumability

**ISO/IEC 25010:2023:** Interaction capability → Appropriateness recognizability, Learnability, Self-descriptiveness, User error protection; Functional suitability → Completeness, Correctness, Appropriateness (`#usable`, `#suitable`)
**Cloud frameworks:** Google Cloud — Document your architecture

## Statement

A consumer can find, understand and use any service without help from the team that runs it. Every service does what it promises, completely and correctly, and says clearly what it promises.

## Why it matters

- A private cloud competes with public clouds on experience; tickets and meetings push departments elsewhere.
- Self-service removes the platform team as a bottleneck.
- A published, tested contract is the only basis for trust between departments.

## Quality Scenarios

| ID | Scenario | Stimulus | Expected response | Measure |
|---|---|---|---|---|
| QG7.1 | Self-service | A consumer needs to provision, modify, upgrade or decommission an instance (R1–R4) | They do it through API, CLI or portal | 0 tickets for routine operations |
| QG7.2 | Discoverability | A consumer looks for a capability | They find the service in the central catalogue | 100% of services listed with documentation, API reference, examples and SLO |
| QG7.3 | Functional correctness | A service is released | It passes its published conformance suite | 100% pass rate before release |
| QG7.4 | Time to first use | A new consumer starts using a service | They succeed using the documentation alone | ≤ N minutes to first successful instance |
| QG7.5 | Error protection | A consumer submits an invalid or risky request | It is rejected with a clear, actionable message | 100% of validation errors explain how to fix them |

## Design Principles

1. **Self-service first.** Every routine operation is available through API, CLI and portal.
2. **One catalogue.** Every service is published in the central catalogue with its documentation, SLO, tier and cost.
3. **Consistent experience.** Services follow the same API conventions, naming, authentication and error format.
4. **Documentation is part of the product.** A service is not released without documentation and working examples.
5. **Conformance proves correctness.** Each service publishes a conformance suite that defines what it promises.
6. **Validate early, explain clearly.** Reject bad input at the edge with messages that say how to fix it.

## Review Checklist

- Can every routine operation be done without a ticket?
- Is the service listed in the catalogue with documentation, examples, SLO, tier and cost?
- Does it follow the platform API conventions?
- Does a published conformance suite pass before every release?
- Can a new consumer succeed from documentation alone?

## Example

A department needs a PostgreSQL database: they find it in the catalogue, read its tier, SLO and cost, provision it through the CLI in minutes using the published example, and never open a ticket.
