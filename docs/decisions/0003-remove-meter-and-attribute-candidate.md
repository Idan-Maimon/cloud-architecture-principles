# ADR-0003 — Remove the Meter & Attribute candidate requirement

**Status:** Accepted
**Date:** 2026-11-16

## Context

R5 Meter & Attribute (*usage and cost of every instance is recorded and attributed to an owner*)
was listed as a candidate requirement, with a note that it may instead be treated as part of
[QG9 Cost Efficiency](../quality-goals/qg09-cost-efficiency.md).

Adding R5 Use ([ADR-0001](0001-requirements.md)) needed a decision on whether to keep
the candidate as R6.

## Decision

Remove Meter & Attribute from the requirements. It is not added as R6.

## Consequences

- The requirements are R1 Provision, R2 Modify, R3 Upgrade, R4 Decommission and R5 Use.
- Metering and cost attribution remain covered as a quality under QG9 Cost Efficiency.
