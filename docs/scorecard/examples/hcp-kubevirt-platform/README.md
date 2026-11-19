# Example — Hosted OpenShift Clusters on KubeVirt (HCP + KubeVirt)

> **Illustrative.** A snapshot of how the service could look after go-live, with its SLO document approved.
> The results show how the scorecard is read; they are not real measurements.
> Internal names (teams, sites, clusters, repositories) are left out on purpose.
> The same service is the SLA framework's [real-service example](https://github.com/Idan-Maimon/sla-framework/tree/main/examples/hcp-kubevirt-platform).

Documents: [service profile](service-profile.md).

## Result

| Deployment | Checks passed | Level | Failed checks |
|---|---|---|---|
| site-a | 27 / 32 | **Silver** | Gold: QG2.6, QG3.4, QG5.1, QG6.3, QG6.4 |
| site-b | 26 / 32 | **Silver** | Gold: the same five, plus QG2.2 |
| site-c | 24 / 32 | **Bronze** | Silver: QG1.4, QG2.5 · Gold: the same six as site-b |

**Service level: Bronze.** site-c is the weakest production deployment, so it sets the level
([rule 2](../../README.md#rules)), even though site-a and site-b are Silver.

| Risk | Count | Checks |
|---|---|---|
| High | 0 | All Bronze checks pass everywhere |
| Medium | 2 | QG1.4 and QG2.5, both on site-c |
| Low | 7 | Five service checks (QG2.6, QG3.4, QG5.1, QG6.3, QG6.4), plus QG2.2 on site-b and site-c |

**Exception:** QG7.2 Opportunism, on all deployments, until 2027-03-31. The platform scheduler can't
yet give capacity back to its owner on demand. It counts as passed while the exception is valid.

**SLO status** (from the SLA framework, shown beside the level): met on all deployments this month.

## Reading the result

| Question | Answer |
|---|---|
| What blocks Silver? | Two Silver checks on site-c: a critical vulnerability open past its deadline (QG1.4), and no restore test this quarter (QG2.5) |
| What blocks Gold, after Silver? | Six Gold checks. The cheapest first: exit plans for the storage and hypervisor providers (QG5.1), and a time-to-first-use test (QG6.4) |
| Is anything urgent? | No High risk. The two Medium risks are on one deployment, with a clear fix |

## Next actions

1. Patch the open critical vulnerability on site-c (QG1.4).
2. Run and record a restore test on site-c (QG2.5). The service then reaches **Silver**.
3. Write exit plan ADRs for the storage and hypervisor providers (QG5.1).
4. Plan a zone-loss exercise for site-b and site-c (QG2.2).
5. Before the exception expires: decide whether the scheduler change for QG7.2 is planned, or renew it.
