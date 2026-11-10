# QG4 — Operability

**ISO/IEC 25010:2023:** Maintainability → Modularity, Analysability, Modifiability, Testability; Interaction capability → Operability (`#operable`, `#maintainable`)
**Cloud frameworks:** AWS — Operational excellence; Google Cloud — Operational excellence, Design for change

## Statement

Every service is operated through automation and can be observed, diagnosed and changed safely and frequently. No production change depends on manual steps or on individual knowledge.

## Why it matters

- At private-cloud scale, manual operations do not scale and cause most incidents.
- Small, frequent, reversible changes lower risk and speed up delivery.
- Fast diagnosis shortens outages more than any other single factor.

## Quality Scenarios

| ID | Scenario | Stimulus | Expected response | Measure |
|---|---|---|---|---|
| QG4.1 | Everything as code | A change to infrastructure or configuration is needed | It is made through a version-controlled, reviewed pipeline | 0 manual changes in production; drift detected and alerted |
| QG4.2 | Observability | A service is running | It emits metrics, logs and traces in the platform-standard format | 100% of services with SLO dashboards and alerts |
| QG4.3 | Frequent change | A team delivers changes | Changes are small, frequent and reversible | DORA metrics tracked: deployment frequency, lead time, change failure rate, time to restore |
| QG4.4 | Diagnosis | An incident occurs | On-call identifies the failing component | ≤ N minutes, using runbooks and dashboards |
| QG4.5 | Rollback | A release causes errors | It is rolled back automatically or with one action | Rollback ≤ N minutes |
| QG4.6 | Learning | An incident is resolved | A blameless post-incident review is held and actions tracked | 100% of major incidents reviewed within N days |

## Design Principles

1. **Automate everything repeatable.** Provisioning, configuration, deployment, scaling and recovery are automated.
2. **Declarative and version-controlled.** The desired state lives in Git; the platform reconciles reality to it.
3. **Observable by default.** Standard metrics, logs and traces are emitted from day one and linked to SLOs.
4. **Small, reversible changes.** Use progressive delivery (canary, blue-green) with automatic rollback.
5. **Runbooks for every alert.** Every alert is actionable and links to a runbook.
6. **Modular services.** Components can be changed, tested and deployed independently.
7. **Learn from failure.** Blameless reviews; actions are tracked to completion.

## Review Checklist

- Is all infrastructure and configuration defined as code and deployed by pipeline?
- Does the service emit standard metrics, logs and traces?
- Are dashboards and alerts linked to SLOs, with a runbook per alert?
- Are DORA metrics tracked?
- Can a release be rolled back in one action?
- Are post-incident reviews held and their actions tracked?

## Example

A messaging service is deployed entirely from Git through a pipeline with canary analysis; when error rates rise during a rollout, it rolls back automatically, pages on-call with a linked runbook, and a blameless review follows within N days.
