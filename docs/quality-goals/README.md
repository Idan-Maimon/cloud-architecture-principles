# Quality Goals

The baseline qualities every service in our private cloud must meet. The vocabulary follows **ISO/IEC 25010:2023**; the operational pillars follow the **AWS Well-Architected Framework** and the **Google Cloud Architecture Framework**.

Measures marked `N` are placeholders to be calibrated. Departments may set stricter targets, never looser ones.

## Mapping

| Goal | ISO/IEC 25010:2023 | AWS Well-Architected | Google Cloud Framework |
|---|---|---|---|
| [QG1 Security](qg01-security.md) | Security | Security | Security, privacy and compliance |
| [QG2 Reliability](qg02-reliability.md) | Reliability | Reliability | Reliability |
| [QG3 Performance Efficiency](qg03-performance-efficiency.md) | Performance efficiency | Performance efficiency | Performance optimization |
| [QG4 Operability](qg04-operability.md) | Maintainability, Interaction capability | Operational excellence | Operational excellence |
| [QG5 Flexibility](qg05-flexibility.md) | Flexibility | — | Design for change, Decouple |
| [QG6 Interoperability](qg06-interoperability.md) | Compatibility | — | — |
| [QG7 Consumability](qg07-consumability.md) | Interaction capability, Functional suitability | — | Document your architecture |
| [QG8 Safety](qg08-safety.md) | Safety | — | — |
| [QG9 Cost Efficiency](qg09-cost-efficiency.md) | Performance efficiency (resource utilization) | Cost optimization | Cost optimization |
| [QG10 Sustainability](qg10-sustainability.md) | — | Sustainability | Sustainability |

All nine ISO/IEC 25010:2023 characteristics and all six pillars of each cloud framework are covered.

## Layout of each goal

Each goal document contains: Statement · Why it matters · Quality Scenarios (stimulus, response, measure) · Design Principles · Review Checklist · Example.

## Sources

- AWS Well-Architected Framework — https://docs.aws.amazon.com/wellarchitected/latest/framework/
- Google Cloud Architecture Framework — https://docs.cloud.google.com/architecture/framework
- ISO/IEC 25010:2023 — https://www.iso.org/obp/ui/#iso:std:iso-iec:25010:ed-2:v1:en
- ISO/IEC 25010 explained (Sonar) — https://www.sonarsource.com/resources/library/iso-iec-25010-explained/
