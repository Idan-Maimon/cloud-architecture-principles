# QG8 — Safety

**ISO/IEC 25010:2023:** Safety → Operational constraint, Risk identification, Fail-safe behaviour, Hazard warning, Safe integration (`#safe`) — new in the 2023 edition
**Cloud frameworks:** AWS and Google Cloud — Reliability (blast radius, guardrails)

## Statement

Every service fails safe, contains the impact of failures and bad changes, and prevents dangerous operations before they happen. Doing the wrong thing is hard; undoing it is possible.

## Why it matters

- In a shared cloud, one destructive action or bad change can affect many departments at once.
- Automation and AI-generated changes operate faster than humans can intervene.
- Preventing harm is cheaper than recovering from it.

## Quality Scenarios

| ID | Scenario | Stimulus | Expected response | Measure |
|---|---|---|---|---|
| QG8.1 | Fail-safe | A dependency fails or returns invalid data | The service degrades in a controlled way without corrupting data | 0 data corruption on dependency failure |
| QG8.2 | Blast radius | A failure or bad change occurs | Impact is contained to one tenant, cell or zone | 0 incidents spanning more than one failure domain |
| QG8.3 | Destructive operation | A consumer deletes an instance or data | Confirmation is required and a protection period applies | Soft-delete / recovery window ≥ N days |
| QG8.4 | Unsafe configuration | A configuration known to be unsafe is submitted | Policy rejects it before it is applied | 100% of baseline policies enforced at admission |
| QG8.5 | Staged rollout | A change is released platform-wide | It rolls out progressively by failure domain | Rollout halts automatically on health regression |
| QG8.6 | Hazard warning | A risky condition develops (capacity, certificate expiry, quorum loss) | Owners are warned before impact | Warning ≥ N days/hours ahead |

## Design Principles

1. **Fail safe, not open.** On uncertainty, stop and protect data rather than continue.
2. **Limit the blast radius.** Partition by tenant, cell and zone; changes and failures stay inside one partition.
3. **Guardrails over gates.** Encode safety rules as policy enforced automatically at admission.
4. **Make destruction reversible.** Soft-delete, protection periods and deletion locks on critical resources.
5. **Roll out progressively.** Change one failure domain at a time, with automatic halt and rollback.
6. **Warn before harm.** Detect and alert on conditions that will lead to incidents.
7. **Constrain automation.** Automated and AI-driven actions run with scoped permissions and rate limits.

## Review Checklist

- What happens to data when each dependency fails?
- What is the largest possible blast radius of a failure or a bad change?
- Are destructive operations confirmed and reversible?
- Are safety policies enforced automatically at admission?
- Do platform-wide changes roll out by failure domain with automatic halt?
- Are automated actions scoped and rate-limited?

## Example

A platform upgrade rolls out one zone at a time and halts automatically when health checks regress; a tenant who deletes a cluster by mistake can restore it within the N-day protection window; admission policy rejects any workload that requests host-level privileges.
