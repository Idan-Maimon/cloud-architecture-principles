# QG1 — Security

**ISO/IEC 25010:2023:** Security → Confidentiality, Integrity, Non-repudiation, Accountability, Authenticity, Resistance (`#secure`)
**Cloud frameworks:** AWS — Security; Google Cloud — Security, privacy and compliance

## Statement

Every service protects its data and its access by default, and can account for every action taken on it. Security is built into the platform and inherited by services; it is not added by each team afterwards.

## Why it matters

- A single weak service exposes every tenant that shares the platform.
- Regulatory and audit obligations can only be met if every action is attributable.
- Secure defaults remove the need for each department to become a security expert.

## Quality Scenarios

| ID | Scenario | Stimulus | Expected response | Measure |
|---|---|---|---|---|
| QG1.1 | Zero trust | A request reaches a service, from inside or outside the network | The request is authenticated and authorised before it is served | 100% of calls authenticated; 0 trust based on network location |
| QG1.2 | Encryption | Data is transmitted or stored | It is encrypted with platform-managed keys | TLS 1.2+ in transit; 100% encrypted at rest |
| QG1.3 | Accountability | An administrative or data-plane action is performed | It is recorded with who, what and when, in an immutable log | 100% of actions logged; retained ≥ N months |
| QG1.4 | Resistance | A vulnerability is published that affects a service | The service is patched within the deadline | Critical ≤ N days; high ≤ N days |
| QG1.5 | Least privilege | A user or workload is granted access | It receives only the permissions it needs, for a limited time | 0 standing admin privileges; access reviewed every N months |
| QG1.6 | Secret handling | A service needs a credential | It obtains it from the platform secret store at runtime | 0 secrets in code, images or Git |

## Design Principles

1. **Identity is the perimeter.** Every human and workload has an identity issued by the platform identity provider; the network is not a trust boundary.
2. **Secure by default.** Encryption, authentication, audit logging and hardened baselines are on by default and cannot be switched off by consumers.
3. **Least privilege, just in time.** Grant the minimum permission for the minimum time; elevate through an audited request.
4. **Secrets never live in code.** Credentials are issued and rotated by the platform secret store.
5. **Everything is audited.** Every action is attributable to an identity and recorded where it cannot be altered.
6. **Shift security left.** Security scanning (code, dependencies, images, configuration) runs in every pipeline and blocks release on critical findings.
7. **Assume breach.** Segment tenants and services so that a compromise is contained.

## Review Checklist

- Is every endpoint authenticated and authorised through the platform identity provider?
- Is all data encrypted in transit and at rest?
- Are all actions audit-logged to the central, immutable log?
- Are there any secrets in code, images or repositories?
- Does the pipeline block release on critical vulnerabilities?
- Are tenants isolated from each other?

## Example

A database service authenticates every client through OIDC-issued workload identities, encrypts storage with keys from the platform KMS, writes every DDL and access event to the central audit log, and is rebuilt from a patched image within N days of a critical CVE.
