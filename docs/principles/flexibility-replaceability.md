# Flexibility (Replaceability)

**Q42 / ISO 25010:2023:** Flexibility → Replaceability, Adaptability (`#flexible`)

## Statement

Every service and infrastructure component depends only on the *capability* it consumes, never on the *implementation* behind it. Any underlying component (compute, storage, network, database, messaging, identity, observability) can be replaced by another implementation of the same capability without redesigning the services that use it.

## Why it matters

- No lock-in to a vendor, hypervisor, cloud or hardware generation.
- Freedom to change cost, sovereignty, licensing or sourcing strategy without a migration programme.
- Technology can be renewed one layer at a time instead of all at once.

## Quality Scenarios

| ID | Scenario | Stimulus | Expected response | Measure |
|---|---|---|---|---|
| FX-1 | Replace an implementation | A capability provider is replaced (e.g. one hypervisor with another, a VM with bare metal or a cloud instance, one storage vendor with another) | Consuming services keep working unchanged | 0 code changes in consumers; changes limited to the provider adapter and its configuration |
| FX-2 | Add a provider | A new implementation of an existing capability is introduced | It becomes available through the existing contract | Onboarding touches only the new adapter; no changes to the platform core or to consumers |
| FX-3 | Run providers side by side | Two implementations of the same capability serve production together | Consumers can't tell them apart, except for advertised characteristics (performance class, location, cost) | The same conformance suite passes on every provider |
| FX-4 | Exit a provider | A strategic decision is made to leave a vendor or cloud | Workloads are moved within a planned window | Exit plan documented per provider; exit effort estimated and bounded |

## Design Principles

1. **Consume capabilities, not products.** Design against "compute", "block storage", "object store" or "message queue", not against a named product. Product names belong in adapters and deployment configuration, never in service logic.
2. **Every capability has an explicit contract.** Each infrastructure capability exposes a versioned, documented interface: an API, a CRD, or a standard protocol such as S3, Redfish, CSI or OIDC.
3. **Prefer open standards over proprietary APIs.** Where a standard exists, use it. Using a proprietary feature is a recorded architecture decision, with its exit cost stated.
4. **Isolate vendor specifics behind adapters.** Provider-specific code lives in one replaceable module per provider. Nothing outside the adapter may import, call or assume provider internals.
5. **Describe what you need, not where it runs.** Services declare requirements (CPU class, latency, durability, zone spread). Placement and provider selection are platform decisions.
6. **Model the provider as an attribute, not a type.** Inventory, scheduling and billing treat the provider as one property of a resource. They don't have a separate code path per provider.
7. **Conformance over trust.** A provider is accepted only when it passes the capability's conformance suite. That suite is how replaceability is proven.
8. **Keep data portable.** Data is stored in open, exportable formats, with a tested path to move it out.
9. **Every lock-in is an explicit decision.** Lock-in is allowed when it pays off, but it must be recorded as an ADR with its rationale, the exit cost and a review date.

## Review Checklist

- Does any service reference a specific vendor, product or cloud outside an adapter?
- Is there a contract and a conformance suite for each capability the service consumes?
- Could a second provider be added without touching consumers?
- Is every proprietary dependency recorded as an ADR with an exit cost?

## Example

A Kubernetes platform consumes the *compute node* capability. KubeVirt VMs, VMware VMs, bare metal and EC2 are interchangeable providers behind one provisioning contract, and the platform and its tenants are unaware of which one supplied a node.
