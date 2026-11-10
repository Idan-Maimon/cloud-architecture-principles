# QG6 — Interoperability

**ISO/IEC 25010:2023:** Compatibility → Interoperability, Co-existence (`#compatible`)
**Cloud frameworks:** Google Cloud — Decouple your architecture

## Statement

Every service works with others through standard, versioned contracts, and shares infrastructure without degrading its neighbours. Integrating with a service never requires knowledge of its internals.

## Why it matters

- Departments compose solutions from many services; every non-standard interface adds integration cost.
- Breaking changes without notice ripple across the organisation.
- Shared infrastructure is only viable if services co-exist safely.

## Quality Scenarios

| ID | Scenario | Stimulus | Expected response | Measure |
|---|---|---|---|---|
| QG6.1 | Standard interface | A consumer integrates with a service | It uses a documented, versioned API based on open standards | 100% of services expose a versioned API (OpenAPI, gRPC, OIDC, S3, CSI…) |
| QG6.2 | Co-existence | Several services share a cluster, network or storage system | None degrades another | Quotas and limits enforced; 0 cross-service incidents from resource contention |
| QG6.3 | Backward compatibility | A service changes its API | Existing consumers keep working | Breaking changes only in a new version; deprecation period ≥ N months |
| QG6.4 | Event integration | A service needs to notify others of a change | It publishes a documented event to the platform event bus | Event schemas versioned and published |
| QG6.5 | Data exchange | Data moves between services | It uses agreed formats and schemas | 0 bespoke point-to-point formats |

## Design Principles

1. **API first.** Design and publish the contract before the implementation.
2. **Use open standards.** Prefer industry protocols and formats over custom ones.
3. **Version everything.** APIs, events and schemas are versioned; breaking changes create a new version.
4. **Publish a deprecation policy.** Old versions are supported for a published period, and consumers are notified.
5. **Integrate through contracts, not databases.** No service reads another service's data store directly.
6. **Share safely.** Every shared resource has quotas, limits and isolation.

## Review Checklist

- Is the service's API documented, versioned and based on an open standard?
- Is there a published deprecation policy?
- Does any consumer depend on internals (database, file layout, private endpoints)?
- Are event and data schemas versioned and published?
- Are quotas and limits set on shared resources?

## Example

An identity service exposes standard OIDC and SCIM endpoints, so every other service integrates without custom code; when it introduces a v2 API, v1 remains supported for N months and consumers are notified through the service catalogue.
