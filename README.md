# Cloud Architecture Principles

Principles, quality goals and design guidance for how services and infrastructure are designed and implemented across our private cloud.

**Audience:** engineers, service developers and architects.

## Contents

| Area | Path | Purpose |
|---|---|---|
| Requirements | [docs/requirements](docs/requirements/README.md) | Business operations every cloud service must provide |
| Quality goals | [docs/quality-goals](docs/quality-goals/README.md) | Baseline qualities, with measurable scenarios |
| Principles | [docs/principles](docs/principles) | Cross-cutting design principles |
| Decisions | [docs/decisions](docs/decisions) | Architecture Decision Records (ADRs) |
| Checklists | [docs/checklists](docs/checklists) | Review checklists for architects |
| Presentations | [presentations](presentations) | Slide decks |
| Diagrams | [diagrams](diagrams) | Diagram sources |

## Quality Goals

| ID | Goal |
|---|---|
| QG1 | [Security](docs/quality-goals/qg01-security.md) |
| QG2 | [Reliability](docs/quality-goals/qg02-reliability.md) |
| QG3 | [Performance Efficiency](docs/quality-goals/qg03-performance-efficiency.md) |
| QG4 | [Operability](docs/quality-goals/qg04-operability.md) |
| QG5 | [Flexibility](docs/quality-goals/qg05-flexibility.md) |
| QG6 | [Interoperability](docs/quality-goals/qg06-interoperability.md) |
| QG7 | [Consumability](docs/quality-goals/qg07-consumability.md) |
| QG8 | [Safety](docs/quality-goals/qg08-safety.md) |
| QG9 | [Cost Efficiency](docs/quality-goals/qg09-cost-efficiency.md) |
| QG10 | [Sustainability](docs/quality-goals/qg10-sustainability.md) |

## Principles

- [Cross-cutting principles](docs/principles/cross-cutting.md)

## Sources

### Quality frameworks

- [ISO/IEC 25010:2023 — Product quality model](https://www.iso.org/obp/ui/#iso:std:iso-iec:25010:ed-2:v1:en)
- [ISO/IEC 25010 explained (Sonar)](https://www.sonarsource.com/resources/library/iso-iec-25010-explained/)
- [AWS Well-Architected Framework](https://docs.aws.amazon.com/wellarchitected/latest/framework/) — [Cost optimization design principles](https://docs.aws.amazon.com/wellarchitected/latest/framework/cost-dp.html)
- [Google Cloud Architecture Framework](https://docs.cloud.google.com/architecture/framework)
- [Q42 — arc42 quality model](https://quality.arc42.org)

### From definition to practice

- [SEI — ATAM: Method for Architecture Evaluation (Kazman, Klein, Clements)](https://www.sei.cmu.edu/documents/629/2000_005_001_13706.pdf)
- [Architecture Tradeoff Analysis: Picking Your Poison (Carefully)](https://www.architectviewmaster.com/blog/architecture-tradeoff-analysis-picking-your-poison-carefully/)
- [DataKnobs — ATAM Guide](https://www.dataknobs.com/blog/architecture/atam/)
- [Thoughtworks — Fitness function-driven development](https://www.thoughtworks.com/insights/articles/fitness-function-driven-development)
- [Architecture Fitness Functions (Software Architecture wiki)](https://synchronium.github.io/software-architecture-wiki/concepts/fitness-functions.html)
- [NILUS — Fitness Functions in Evolutionary Architecture](https://www.nilus.be/blog/architecture_fitness_functions_in_evolutionary_architecture/)
- [AWS — Using Cloud Fitness Functions to Drive Evolutionary Architecture](https://aws.amazon.com/blogs/architecture/using-cloud-fitness-functions-to-drive-evolutionary-architecture/)
- [Architects, Don't Skip Leg Day: Fitness Functions Matter](https://medium.com/@oscarvanderleij/architects-dont-skip-leg-day-fitness-functions-matter-ef16ab9ed012)
- [AWS re:Invent ARC204 — Scaling Well-Architected Reviews through the enterprise](https://d1.awsstatic.com/events/Summits/reinvent2022/ARC204_Scaling-AWS-Well-Architected-Reviews-through-the-enterprise.pdf)
- [Well-Architected Review Buyer Guide 2026](https://www.factualminds.com/blog/aws-well-architected-review-buyer-guide-2026/)
- [The Serverless Edge — Making well-architected reviews work for organisations](https://theserverlessedge.com/how-to-make-well-architected-work-for-organisations-introducing-the-scorp-review-cycle-part-1/)
- [Spotify for Backstage — Soundcheck and a healthier tech culture](https://backstage.spotify.com/discover/blog/soundcheck-healthier-tech-culture)
- [Platform Engineering Golden Paths: Internal Developer Portals in 2026](https://www.ainformat.com/detail/2698)
- [Backstage vs Port vs Cortex](https://wetheflywheel.com/en/comparisons/backstage-vs-port-vs-cortex/)
