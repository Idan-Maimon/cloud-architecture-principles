# Requirements

A requirement is a **business operation** a cloud service delivers, not how it is built. How a service fulfils these operations is an architecture decision; how well it fulfils them is a [quality goal](../quality-goals/README.md).

Every cloud service in the private cloud (compute, storage, database, Kubernetes, messaging, and so on) must offer these operations through a self-service API:

| ID | Requirement | Business operation |
|---|---|---|
| R1 | **Provision** | A consumer can obtain an instance of the service on demand |
| R2 | **Modify** | A consumer can change an instance: size, configuration, scale |
| R3 | **Upgrade** | The provider can renew an instance (patches, versions) throughout its life |
| R4 | **Decommission** | A consumer can release an instance, and its resources and data are disposed of |
| R5 | **Meter & Attribute** *(candidate)* | Usage and cost of every instance is recorded and attributed to an owner |
| R6 | **Consume/ Something else** | A consumer can Interact with the service |

R5 is a candidate: it may instead be treated as part of [QG9 Cost Efficiency](../quality-goals/qg09-cost-efficiency.md).
R6 is a candidate: it may be changed or merged into R1 as a new or upgraded Requirement
