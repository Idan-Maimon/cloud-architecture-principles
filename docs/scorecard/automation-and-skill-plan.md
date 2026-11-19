# Scorecard Automation and Claude Skill — Plan

> **Status:** DRAFT, for discussion. Not yet agreed.

How the [scorecard](README.md) moves from documents to working tooling: what runs as automation,
and what a Claude skill does.

## The boundary

A Claude skill is a good fit for the work that needs judgment and writing. It should **not** be the
engine that produces the rankings, reports and alerts. Those must run on a schedule, give the same answer
every time, and be auditable without anyone starting a Claude session. A level that could change depending
on how a model reads the data would not be trusted, and it shouldn't be.

## The split

| Part | Built as | Does |
|---|---|---|
| **Scoring engine** | Plain code in the platform tooling | Reads check results, applies exceptions and "not applicable", calculates levels per deployment and per service, and publishes them as Prometheus metrics |
| **Dashboards, alerts, monthly report** | Grafana JSON, Prometheus alert rules, a scheduled report job | Run without Claude. Example alerts: a deployment dropped a level, a new High risk, an exception expires within 30 days |
| **Claude skill** | `SKILL.md` plus the scoring script, bundled together | The work people do: onboarding, reviews, exceptions, explanations, and generating or updating the automation above |

## What the skill does

| Task | How |
|---|---|
| **Onboard a service** | Interviews the service owner and writes the [service profile](templates/service-profile.md), the same way the arc42 skills work through a section |
| **Run a review** | Leads the [scorecard review](review-guide.md): utility tree ratings, the review checks, risks. Then drafts the [exception](templates/exception.md) ADRs |
| **Explain a score** | Answers questions such as "why is this service Bronze and what do we fix first?" It runs the *same* scoring script, so its answer always matches the dashboard |
| **Build the automation** | Generates Grafana dashboards, alert rules, ACM policy skeletons and CI checks from the [check catalogue](check-catalogue.md), delivered as pull requests for people to review |

## Ground rules

- **The check catalogue is the only source of checks.** The skill reads it and never invents checks.
- **People approve** exceptions and anything that goes to production.
- **Nothing internal in the skill.** This repository is public; cluster names, endpoints and other
  internal details stay in configuration in internal repositories.

## Build order

1. **A machine-readable catalogue** (`checks.yaml`) generated from [check-catalogue.md](check-catalogue.md),
   plus the scoring script and the metric definition, for example
   `scorecard_check_passed{service, deployment, check, level}`. Everything else depends on these.
2. **Real Grafana dashboards and alert rules** built from that metric, replacing the
   [example images](README.md#dashboards).
3. **The skill**, wrapping onboarding, review and explanation, and bundling the scoring script.

If the skill came first, Claude would end up doing the scoring itself, which is the part it shouldn't own.
