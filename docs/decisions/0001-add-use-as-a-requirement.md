# ADR-0001 — Add R5 Use as a requirement

**Status:** Accepted
**Date:** 2026-11-16

## Context

The requirements were R1 Provision, R2 Modify, R3 Upgrade and R4 Decommission: the lifecycle
operations on an instance. None of them covers the most basic thing a consumer expects: that the
instance they obtained can be accessed and used.

The [requirements and qualities](../principles/requirements-and-qualities.md) principle says *a
quality is always measured on a requirement*. Availability and data-plane latency were measured on a
"Running instance" row that was not a requirement, which broke that principle.

PR #1 raised the same gap: the people this is presented to will not separate requirements from
qualities, so "is the service still working?" has to be visible as a requirement.

Industry sources treat using the service as its own step:

- NIST SP 500-292 lists the consumer's activities as requesting a service, then using it.
- The Open Service Broker API has an explicit *bind* operation that gives the consumer access to
  the instance, next to provision, update and deprovision.
- Requirements engineering separates what a system does (requirement) from how well it does it
  (quality, e.g. availability).

## Decision

Add **R5 Use**: *a consumer can access the instance and use it for its purpose (run workloads,
read and write data, call its API) for as long as it exists.*

Availability (uptime) and data-plane latency are qualities measured on R5.

## Consequences

- Every SLO category is now a requirement; availability is no longer a special case.
- The "Running instance" row in the requirements × qualities matrix, QG2 and QG3 must be renamed to
  R5 Use, and the SLA framework's "Availability" category aligned with it.
- R5 is no longer available for Meter & Attribute (see [ADR-0002](0002-remove-meter-and-attribute-candidate.md)).

## Alternatives considered

- **Keep "Running instance" as a matrix row only.** Rejected: it leaves the basic expectation out
  of the requirements and breaks the requirements-and-qualities principle.
- **Merge it into R1 Provision** (as proposed in PR #1). Rejected: Provision is obtaining an
  instance; Use is what happens afterwards, for its whole life.
- **Number it R1 and renumber the rest.** Rejected: R1–R4 are already used in the SLA framework's
  templates and examples.
