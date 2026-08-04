## Copilot instructions for ONTAP tools for VMware vSphere documentation

### Repository overview
Product: ONTAP tools for VMware vSphere

*ONTAP tools for VMware vSphere* is a set of tools for virtual machine lifecycle management in VMware environments. It is deployed as an *OVA* and combines a vSphere *remote plug-in*, *ONTAP tools Manager*, and related services for datastore provisioning, storage policy-based management, and protection workflows.

### Repository structure
- `_include/` – Reserved for shared include content; currently contains only a placeholder README for future reusable snippets.
- `automation/` – REST API concepts, first-call guidance, implementation details, and API reference content.
- `concepts/` – Product overview, core terminology, and RBAC concepts for ONTAP and vCenter environments.
- `configure/` – vCenter onboarding, storage backend setup, datastore creation, privilege configuration, network access, and discovery tasks.
- `deploy/` – Prerequisites, pre-deployment checks, appliance deployment, HA workflow, quick start, and deployment troubleshooting.
- `manage/` – Day-2 administration including services, certificates, passwords, backup and recovery, datastore operations, maintenance console, and appliance settings.
- `media/` – Images and UI captures referenced by the documentation pages.
- `migrate/` – Migration workflows from earlier ONTAP tools deployments, including SRA and VASA migration topics.
- `protect/` – Disaster recovery and protection tasks for SRA, VMware Live Site Recovery, protection groups, mappings, and host cluster protection.
- `redirect/` – Redirect pages that preserve older permalinks and point them to current content locations.
- `release-notes/` – Release notes, what's new content, and feature comparison information.
- `upgrade/` – Upgrade procedures and upgrade error code reference topics.

### Product-specific context
**Architecture and components:**
- *ONTAP tools for VMware vSphere* is deployed as a separate virtual appliance using the vSphere *remote plug-in* architecture rather than running inside vCenter.
- The appliance exposes a single *ONTAP tools IP* that fronts the web UI, Swagger page, and REST API through an internal load balancer.
- *ONTAP tools Manager* is the web console for appliance settings, managed vCenter Server instances, storage backends, certificates, passwords, alerts, jobs, and log bundles.
- Optional services include *VASA Provider* for storage policy-based management and *vVols*, and *Storage Replication Adapter (SRA)* for disaster recovery integration with *VMware Live Site Recovery*.
- The ONTAP tools REST API is separate from the ONTAP cluster REST API; ONTAP tools uses the ONTAP REST API as a client for storage operations.
- The product supports single-node deployments for core services and expanded *HA* deployments for resiliency and scale; HA nodes must remain on the same subnet for inter-node communication.

**Key concepts:**
- A *storage backend* is the ONTAP storage infrastructure used by ESXi hosts for datastore operations and discovery.
- *Global storage backends* are added in *ONTAP tools Manager* with ONTAP cluster credentials and mapped to vCenter instances; this model is important for multitenant and *vVols* management.
- *Local storage backends* are added in the ONTAP tools user interface with cluster or *SVM* credentials and are limited to a single vCenter context.
- An *SVM* (*storage virtual machine*) is the ONTAP multitenancy boundary that serves data through its own logical resources and network interfaces.
- *VMFS* and *NFS* are the core datastore types supported by the base deployment; *vVols* workflows depend on *VASA Provider* registration and storage policy-based management.
- *SnapMirror active sync* is used in protection content for host cluster protection of *VMFS* datastores and appears with *uniform* and *non-uniform* host access terminology.

**Naming conventions and terminology:**
- Use *ONTAP tools Manager* for the appliance web console and *NetApp ONTAP tools* for the vSphere client plug-in label.
- Use *VASA Provider*, *Storage Replication Adapter (SRA)*, *VMware Live Site Recovery*, *VMFS*, *vVols*, *SVM*, and *VM Storage Policy* exactly as written in the docs.
- Use *storage backend* instead of generic terms like "array" or "storage system" when referring to ONTAP resources managed by the product.
- Distinguish *global* and *local* storage backends because the scope, credential model, and vCenter mapping behavior differ.
- Use *host cluster protection* for *SnapMirror active sync* protection workflows and *datastore protection* for SRA-based disaster recovery workflows.

### Typical user workflows
**Initial deployment:** Plan environment and network requirements → Deploy the OVA appliance → Add a vCenter Server instance to register the remote plug-in and privileges → Add ONTAP storage backends → Provision and manage datastores

**vVols enablement:** Enable *VASA Provider* in *ONTAP tools Manager* → Register the provider with vCenter → Add or associate storage backends → Create *VM Storage Policies* → Provision and manage *vVols* datastores

**Disaster recovery setup:** Enable *SRA* services in *ONTAP tools Manager* → Install and configure the adapter in *VMware Live Site Recovery* → Add vCenter instances and storage backends → Configure protection groups and site mappings → Run test failover and reprotect workflows

**Appliance administration:** Open *ONTAP tools Manager* → Review alerts, jobs, and node status → Manage certificates, passwords, and backups → Adjust appliance settings such as HA or scaling → Download log bundles for troubleshooting
