# Requirements

A requirement is a **business operation** a cloud service delivers, not how it is built. How a service fulfils these operations is an architecture decision; how well it fulfils them is a [quality goal](../quality-goals/README.md).

Every cloud service in the private cloud (compute, storage, database, Kubernetes, messaging, and so on) must offer these operations through a self-service API:

| ID | Requirement | Business operation |
|---|---|---|
| R1 | **Provision** | A consumer can obtain an instance of the service on demand |
| R2 | **Modify** | A consumer can change an instance: size, configuration, scale |
| R3 | **Upgrade** | The provider can renew an instance (patches, versions) throughout its life |
| R4 | **Decommission** | A consumer can release an instance, and its resources and data are disposed of |
| R5 | **Use** | A consumer can access the instance and use it for its purpose (run workloads, read and write data, call its API) for as long as it exists |

## Sources

- [NIST SP 500-292 — Cloud Computing Reference Architecture](https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication500-292.pdf): the cloud consumer requests a service, then uses it
- [Open Service Broker API specification](https://github.com/cloudfoundry/servicebroker/blob/master/spec.md): service lifecycle of provision, update, bind (access), unbind and deprovision
- [Non-functional requirement (Wikipedia)](https://en.wikipedia.org/wiki/Non-functional_requirement): what a system does is a requirement; how well it does it is a quality attribute
- [Google SRE Workbook — Implementing SLOs](https://sre.google/workbook/implementing-slos/): SLOs are written on user-centric actions and critical user journeys
