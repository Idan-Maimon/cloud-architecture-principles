# Scorecard Review

A half-day review for the checks a tool can't measure, and for a first look at a new service.
It borrows the **utility tree** from SEI's [ATAM](https://www.sei.cmu.edu/documents/629/2000_005_001_13706.pdf):
rate each scenario, then spend the time on the ones that matter most and are hardest to achieve.

**When:** before a new service goes to production, after a major change, and once a year.

| Role | Who |
|---|---|
| **Authors** | Architect + service owner |
| **Reviewers** | Dev lead + on-call lead |
| **Approver** | Section leader |

**Bring:** the [service profile](templates/service-profile.md), the service's architecture docs (arc42),
its SLO document, and the current scorecard.

## Agenda (about 4 hours)

| # | Step | Time | What happens |
|---|---|---|---|
| 1 | **Service overview** | 20 min | The service owner presents what the service does, its users, its deployments and its critical dependencies |
| 2 | **Rate the scenarios** | 45 min | For each scenario that applies, rate **importance** to the business and **difficulty** to achieve: High, Medium or Low. This is the utility tree |
| 3 | **Walk the review checks** | 90 min | Go through every check marked *(review)* in the [catalogue](check-catalogue.md) and record pass or fail with evidence |
| 4 | **Analyse High/High scenarios** | 60 min | For each scenario rated High importance and High difficulty, ask how the architecture achieves it. Record **risks**, **sensitivity points** (a decision that a scenario depends on) and **tradeoffs** (a decision that helps one quality and hurts another) |
| 5 | **Wrap up** | 25 min | Agree the outputs below |

The checks marked *(review)* today: QG2.2 Failure containment, QG2.3 Component failure, QG2.6 Overload,
QG3.4 Noisy neighbour, QG6.4 Time to first use, QG6.5 Error protection.

## Outputs

| Output | Goes to |
|---|---|
| Pass or fail for each review check, with evidence and date | The service profile, *Review results* |
| Risks found in step 4 | The service's risk list (arc42 Section 11) |
| Decisions taken or confirmed | ADRs in the service's repository |
| Failed checks the team accepts for now | [Exceptions](templates/exception.md), each with an expiry date |
| Next review date | The service profile |

**Done when:** every review check has a result, and every failed check is either planned for a fix or
covered by an exception.
