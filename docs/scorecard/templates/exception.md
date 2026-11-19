# ADR-`<NNNN>` — Exception: `<check ID>` on `<service / deployment>`

> An accepted failed check. Stored with the service's other ADRs. While it is approved and not expired,
> the check counts as passed and is shown on the dashboard as an exception. Replace everything in `<…>`.

| | |
|---|---|
| **Status** | Proposed / Approved / Expired |
| **Check** | `<QG7.2 Opportunism>` ([catalogue](../check-catalogue.md)) |
| **Deployments** | `<all / site-c/cluster-03>` |
| **Risk accepted** | `<High / Medium / Low, from the check's level>` |
| **Approved by** | `<section leader>` |
| **Approval date** | |
| **Expires** | `<date: at most 6 months for High risk, 12 months otherwise>` |

## Context

`<Why the check fails today, and why it can't be fixed now.>`

## Decision

We accept that `<check>` fails on `<deployments>` until `<expiry date>`.

## Mitigation

`<What reduces the risk in the meantime.>`

## Plan to pass

| Action | Owner | Due |
|---|---|---|
| `<…>` | | |

When the plan is done, the check passes and this ADR is closed. If it expires first, the check fails
again until the exception is renewed or the check passes.
