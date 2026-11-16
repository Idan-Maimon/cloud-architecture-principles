# ADR-0001 — Requirements: R1–R5 business operations

**Status:** Accepted
**Date:** 2026-11-10 · **Updated:** 2026-11-16 (R5 Use added)

## Context

Every cloud service in the private cloud (compute, storage, database, Kubernetes, messaging, and so
on) needs a common baseline: what any consumer can expect to do with it, regardless of the
technology behind it. Without one, each team describes its service in its own terms, and
qualities such as reliability or performance have nothing common to be measured on.

## Decision

1. **A requirement is a business operation** a cloud service delivers, not how it is built. How a
   service fulfils an operation is an architecture decision; how well it fulfils it is a
   [quality goal](../quality-goals/README.md).
2. Every cloud service provides these five requirements:

| ID | Requirement | Business operation |
|---|---|---|
| R1 | **Provision** | A consumer can obtain an instance of the service on demand |
| R2 | **Modify** | A consumer can change an instance: size, configuration, scale |
| R3 | **Upgrade** | The provider can renew an instance (patches, versions) throughout its life |
| R4 | **Decommission** | A consumer can release an instance, and its resources and data are disposed of |
| R5 | **Use** | A consumer can access the instance and use it for its purpose (run workloads, read and write data, call its API) for as long as it exists |

### Why these five

- **R1–R4 are the lifecycle of an instance.** Obtain it, change it, keep it current, release it.
  They match the self-service model in the NIST definition of cloud computing (on-demand
  self-service) and the lifecycle in the Open Service Broker API (provision, update, deprovision).
  Upgrade is included because in a private cloud the provider, not the consumer, keeps instances
  patched and current.
- **R5 Use was added on 2026-11-16** (raised in PR #1). R1–R4 did not cover the most basic
  expectation: *the instance I got works and I can use it*. People who don't separate requirements
  from qualities would not see that expectation anywhere, and availability was measured on a
  "Running instance" row that was not a requirement, which broke
  [ADR-0002](0002-quality-measured-on-a-requirement.md). NIST SP 500-292 lists *using* the service
  as a consumer activity after requesting it, and the Open Service Broker API has an explicit
  *bind* operation that gives the consumer access to the instance.

## Consequences

- Every service is described with the same five operations, so services can be compared and
  reviewed the same way.
- Every quality, including availability, is measured on one of the five requirements. Availability
  (uptime) and data-plane latency are measured on R5.
- The "Running instance" row in the requirements × qualities matrix, QG2 and QG3 must be renamed to
  R5 Use, and the SLA framework's "Availability" category aligned with it.
- Metering and cost attribution are not a requirement (see
  [ADR-0003](0003-remove-meter-and-attribute-candidate.md)).

## Alternatives considered

- **Describe requirements per service type** (a VM's operations differ from a database's).
  Rejected: the details differ, but the five operations are the same for every service, and a
  common baseline is the point.
- **Keep "Running instance" as a matrix row only, instead of R5.** Rejected: it leaves the most
  basic expectation out of the requirements.
- **Merge Use into R1 Provision** (as proposed in PR #1). Rejected: Provision is obtaining an
  instance; Use is what happens afterwards, for its whole life.
- **Number Use as R1 and renumber the rest.** Rejected: R1–R4 are already used in the SLA
  framework's templates and examples.

## Sources

- [NIST SP 800-145 — The NIST Definition of Cloud Computing](https://nvlpubs.nist.gov/nistpubs/legacy/sp/nistspecialpublication800-145.pdf)
- [NIST SP 500-292 — Cloud Computing Reference Architecture](https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication500-292.pdf)
- [Open Service Broker API specification](https://github.com/cloudfoundry/servicebroker/blob/master/spec.md)
- [Non-functional requirement (Wikipedia)](https://en.wikipedia.org/wiki/Non-functional_requirement)
