# Requirements and Qualities

How [requirements](../requirements/README.md) and [quality goals](../quality-goals/README.md) relate, and how each combination is checked in practice.

## The principle

**A quality is always measured on a requirement.**

- A **requirement** is a business operation: Provision, Modify, Upgrade, Decommission. On its own it is pass/fail: the operation happened or it did not.
- A **quality** says *how well* the operation must happen: how fast, how reliably, how securely.
- Neither is useful alone. A quality with no operation to apply to cannot be measured; a requirement with no quality cannot be judged.

This follows the quality attribute scenario form from SEI's ATAM:

> **Stimulus** (an operation is triggered) → **Response** (the system handles it) → **Response measure** (how well)

### Example

> *Stimulus:* a tenant cluster upgrade is triggered (**R3 Upgrade**). *Response:* the upgrade completes. *Response measure:* ≤ 1.5 h (**QG3 Performance Efficiency** — time behaviour).

If the upgrade takes 3 hours, it misses the measure. In the [SLA framework](https://github.com/Idan-Maimon/sla-framework) this is an SLO on the Upgrade operation, and the miss consumes error budget.

## Two kinds of quality, two ways to check them

| Kind | Qualities | Measured per operation? | How it is checked |
|---|---|---|---|
| **Runtime qualities** | QG2 Reliability, QG3 Performance Efficiency | Yes: each operation has a success rate and a duration | **SLOs and error budgets**, per operation, using the [SLA framework](https://github.com/Idan-Maimon/sla-framework) |
| **Built-in qualities** | QG1 Security, QG4 Operability, QG5 Flexibility, QG6 Interoperability, QG7 Consumability, QG8 Safety, QG9 Cost Efficiency, QG10 Sustainability | No: they are properties of how the service is built and run | **Fitness functions** (automated checks in pipelines and policy), **scorecards** and **architecture reviews** |

Runtime qualities are what the business sees. Built-in qualities are what make the runtime results achievable and sustainable.

## The matrix

Every service fills this matrix. Each cell says how that quality is checked for that operation.

| | QG2 Reliability | QG3 Performance | Built-in qualities (QG1, QG4–QG10) |
|---|---|---|---|
| **R1 Provision** | SLO: % of provisions that succeed | SLO: time to ready (e.g. p95) | Fitness functions, scorecard, review |
| **R2 Modify** | SLO: % of modifications that succeed | SLO: time to apply | Fitness functions, scorecard, review |
| **R3 Upgrade** | SLO: % of upgrades that succeed | SLO: upgrade duration (e.g. ≤ 1.5 h) | Fitness functions, scorecard, review |
| **R4 Decommission** | SLO: % of decommissions that complete, resources and data disposed | SLO: time to release | Fitness functions, scorecard, review |
| **Running instance** | SLO: availability of what was provisioned | SLO: data-plane latency | Fitness functions, scorecard, review |

The last row covers the instance itself once provisioned (for example, "my VM keeps running"), which consumers experience between operations.

## What this means in practice

1. **Organise SLOs by operation, not by quality.** The business asks "how is my upgrade doing?", not "how is our performance efficiency?".
2. **Targets come from data.** SLO numbers are set per operation from measured performance, following the SLA framework, not from a fixed table per quality.
3. **Built-in qualities are checked continuously, not reported monthly.** They live in pipelines, admission policy and scorecards, and fail fast when broken.
4. **Every cell has an owner.** An empty cell means a quality nobody checks for that operation.

## Related

- [Requirements](../requirements/README.md)
- [Quality goals](../quality-goals/README.md)
- [SLA framework](https://github.com/Idan-Maimon/sla-framework)
- [SEI — ATAM: Method for Architecture Evaluation](https://www.sei.cmu.edu/documents/629/2000_005_001_13706.pdf)
