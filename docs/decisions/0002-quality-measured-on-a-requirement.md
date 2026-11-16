# ADR-0002 — A quality is always measured on a requirement

**Status:** Accepted
**Date:** 2026-11-11

## Context

The private cloud has [requirements](../requirements/README.md) (business operations, see
[ADR-0001](0001-requirements.md)) and ten [quality goals](../quality-goals/README.md). On their own,
neither can be checked: a quality with no operation to apply to cannot be measured, and a
requirement with no quality is only pass/fail.

Qualities are also of two different kinds. Some are visible every time an operation runs (did it
work, how long did it take); others are properties of how the service is built and run (security,
cost, how easy it is to change), and cannot be counted as good and bad events.

## Decision

1. **A quality is always measured on a requirement.** This follows the quality attribute scenario
   form from SEI's ATAM: *stimulus* (an operation is triggered) → *response* (the system handles
   it) → *response measure* (how well).
2. Qualities are checked in one of two ways:

| Kind | Qualities | How it is checked |
|---|---|---|
| **Runtime qualities** | QG2 Reliability, QG3 Performance Efficiency | **SLOs and error budgets**, per requirement, using the [SLA framework](https://github.com/Idan-Maimon/sla-framework) |
| **Built-in qualities** | QG1, QG4–QG10 | **Fitness functions** (automated checks in pipelines and policy), **scorecards** and **architecture reviews** |

3. Every service fills the requirements × qualities matrix in
   [Requirements and qualities](../principles/requirements-and-qualities.md). Each cell says how
   that quality is checked for that requirement, and has an owner.

## Consequences

- SLOs are organised by requirement, not by quality: the business asks "how is my upgrade doing?",
  not "how is our performance efficiency?".
- Built-in qualities are checked continuously in pipelines, admission policy and scorecards, not
  reported monthly.
- An empty matrix cell shows a quality nobody checks for that requirement.

## Alternatives considered

- **Measure and report each quality goal on its own** (a reliability report, a performance
  report). Rejected: the numbers have no operation behind them, so they are hard to act on and
  don't match what consumers experience.
- **Check every quality with SLOs.** Rejected: built-in qualities such as security or flexibility
  are not good and bad events over time; they are checked by automated rules and reviews.

## Sources

- [SEI — ATAM: Method for Architecture Evaluation](https://www.sei.cmu.edu/documents/629/2000_005_001_13706.pdf)
- [Google SRE Workbook — Implementing SLOs](https://sre.google/workbook/implementing-slos/)
- [Thoughtworks — Fitness function-driven development](https://www.thoughtworks.com/insights/articles/fitness-function-driven-development)
