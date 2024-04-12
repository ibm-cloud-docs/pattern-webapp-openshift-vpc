---

copyright:
  years: 2024
lastupdated: "2024-01-23"

subcollection: <repo-name>

keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Architecture decisions for networking
{: #networking-architecture}

<!-- Below is a placeholder for all compute domain decisions.  Remove the domains that are not in scope.  If there are decisions
that need to be added (e.g. platform dependent) add additional rows-->

The following tables summarize the networking architecture decisions for the web app multi-zone resiliency pattern.

## Architecture decisions for enterprise connectivity
{: #enterprise-connectivity}

The following are architecture decisions for enterprise connectivity for this design.

| Architecture decision | Requirement | Option | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- | -------------- |
| Management connectivity | Provide secure, encrypted connectivity to the cloud’s private network for management purposes. | text | text | text. |
| Enterprise connectivity | Provide connectivity between client enterprise and IBM Cloud. | text | text | text. |
{: caption="Table 1. Architecture decisions for enterprise connectivity" caption-side="bottom"}

## Architecture decisions for BYOIP and Edge Gateways
{: #byoip-edge-gateways}

The following are network BYOIP and edge gateay architecture decisions for this design.

| Architecture decision | Requirement | Option | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- | -------------- |
| BYOIP approach | Provide capability for bring your own IP (BYOIP) to IBM Cloud. | text | text | text |
| Edge gateways | Capability to provide edge routing services and possible tunnel termination. | text | text | text |
{: caption="Table 2. Architecture decisions for bring your own IP and edge gateways" caption-side="bottom"}

## Architecture decisions for network segmentation and isolation
{: #network-segmentation-isolation}

The following are network segmentation and isolation architecture decisions for this design.

| Architecture decision | Requirement | Option | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- | -------------- |
| Network segmentation and isolation | Ability to provide network isolation across workloads. | text | text | text |
{: caption="Table 3. Architecture decisions for network segmentation and isolation" caption-side="bottom"}

## Architecture decisions for cloud native connectivity
{: #cloud-native-connectivity}

The following are cloud native connectivity architecture decisions for this design.

| Architecture decision | Requirement | Option | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- | -------------- |
| Cloud native connectivity (to cloud services) | Provide secure connection to Cloud Services | * VPC Gateway + Virtual Private Endpoints (VPE) \n * Private Cloud Service endpoints \n * Public Cloud Service Endpoints | text | text |
| Multi-landing zone connectivity | Connect two or more VPCs over a private network /n Connectectivity between classic, VPCs and/or Power Virutal Server| * Global Transit Gateway \n * Local Transit Gateway (TGW) | text | text |
{: caption="Table 4. Architecture decisions for cloud native connectivity" caption-side="bottom"}

## Architecture decisions for load balancing
{: #network-load-balancing}

The following are load balancing architecture decisions for this design.

| Architecture decision | Requirement | Option | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- | -------------- |
| Global load balancing | Load balancing over the public network across two regions in the event of an outage (DR) for failover to the other region. | text | text |text|
| Load balancing (public) | Load balancing workloads across multiple workload instances or zones over the public network. | text | text |text|
| Load balancing (private) | Load balancing workloads across multiple workload instances or zones over the private network. | text | text |text|
{: caption="Table 5. Architecture decisions for load balancing" caption-side="bottom"}

## Architecture decisions for content delivery network
{: #network-content delivery network}

The following are content delivery network architecture decisions for this design.

| Architecture decision | Requirement | Option | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- | -------------- |
| Content delivery network | Provide ability to cache frequently accessed content at location nearest to the user | text | text | text |
{: caption="Table 6. Architecture decisions for content delivery network" caption-side="bottom"}


## Architecture decisions for domain name system
{: #dns}

The following are domain name system (DNS) architecture decisions for this design.

| Architecture decision | Requirement | Option | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- | -------------- |
| Public DNS | Provide DNS resolution to support the use of hostnames instead of IP addresses for applications | text | text | text |
| Private DNS | Provide DNS resolution within IBM Cloud's private network | text| text | text |
{: caption="Table 7. Architecture decisions for domain name system" caption-side="bottom"}
