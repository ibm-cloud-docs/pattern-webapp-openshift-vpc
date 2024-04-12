---

copyright:
  years: 2024
lastupdated: "2024-01-23"

subcollection: <repo-name>

keywords:

authors:
- name: Doug Eppard

# The release that the reference architecture describes
version: 1.0

# Use if the reference architecture has deployable code.
# Value is the URL to land the user in the IBM Cloud catalog details page for the deployable architecture.
# See https://test.cloud.ibm.com/docs/get-coding?topic=get-coding-deploy-button
deployment-url:

docs: /docs/pattern-sap-on-powervs

content-type: reference-architecture

---
<!--
The following line inserts all the attribute definitions. Don't delete.
-->
{{site.data.keyword.attribute-definition-list}}

<!--
Don't include "reference architecture" in the following title.
Specify a title based on a use case. If the architecture has a module
or tile in the IBM Cloud catalog, match the title to the catalog. See
https://test.cloud.ibm.com/docs/solution-as-code?topic=solution-as-code-naming-guidance.
-->

# SAP on VPC <!-- H1 -->
{: #sap-on-vpc}
{: toc-content-type="reference-architecture"}
{: toc-version="1.0"}

<!--
The IDs, such as {: #title-id} are required for publishing this reference architecture in IBM Cloud Docs. Set unique IDs for each heading. Also include
the toc attributes on the H1, repeating the values from the YAML header.
 -->

<!-->:information_source: **Tip:** For more information about this template, see [Creating reference architectures](https://test.cloud.ibm.com/docs/writing?topic=writing-reference-architectures).-->

Include a short description, summary, or overview in a single paragraph that follows the title.

After the introduction, include a summary of the typical use case for the architecture. The use case might include the motivation for the architecture composition, business challenge, or target cloud environments.


## Architecture diagram <!-- this is an H2 -->
{: #architecture-diagram}

<!--Include the architecture diagram SVG file that was created by using drawio and the IBM2 library.

![Enter image alt text here.](example-architecture-diagram.svg "Title text that shows on hover here"){: caption="Figure 1. Pattern-name solution architecture" caption-side="bottom"}

If you have a list or text to describe the diagram, include it here.you may have more than one diagram -->

Figure 1 illustrates...overview text here

![A diagram of a computer network Description automatically
generated](./image1.svg)

Figure 1 Pattern-name solution architecture<!-- this is the diagram caption -->

Figure 1 detailed description goes here


Figure 2 illustrates ....overview text here.

![A diagram of a computer network Description automatically
generated](./image2.svg)

Figure 2 Pattern-name solution architecture

figure 2 detailed diagram description here

## Design scope <!-- H2 -->
{: #design-scope}

Following the [Architecture Framework](/docs/architecture-framework?topic=architecture-framework-taxonomy), pattern-name covers design considerations and architecture decisions for the following aspects and domains:

<!-- include all aspectsand domains relavant to the pattern below -->
- **Compute:** Bare Metal and Virtual infrastructure

- **Storage:** Primary, Backup, Archive and Migration

- **Networking:** Enterprise Connectivity, Edge Gateways, Segmentation and Isolation, Cloud Native Connectivity and Load Balancing

- **Security:** Data, Identity and Access Management, Infrastructure and Endpoint, Threat Detection and Response

- **Resiliency:** Backup and Restore, Disaster Recovery, High Availability

- **Service Management:** Monitoring, Logging, Alerting, Management/Orchestration

The Architecture Framework, described in [Introduction to the Architecture Framework](/docs/architecture-framework?topic=architecture-framework-intro), provides a consistent approach to design cloud solutions by addressing requirements across a pre-defined set of aspects and domains, which are technology-agnostic architectural areas that need to be considered for any enterprise solution. It can be used as a guide to make the necessary design and component choices to ensure you have considered applicable requirements for each aspect and domain. After you have identified the applicable requirements and domains that are in scope, you can evaluate and select the best fit for purpose components for your enterprise cloud solution.

The Figure 3 shows the domains that are covered in this solution.

<!-- use the draw.io framework template to create your heatmap image, located here https://ibm.ent.box.com/file/1389368500379 -->
![A diagram of a computer network Description automatically
generated](./image3.svg)

Figure 3 design scope

## Requirements <!-- H2 -->
{: #requirements}

<!-- insert the requirements table, below is an example -->

The following represents a baseline set of requirements which we believe are applicable to most clients and critical to successful SAP deployment.

| Aspect | Requirement |
|---------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Network| Enterprise connectivity to customer data center(s) to provide access to applications from on-prem|
| | Map and convert existing customer SAP Network functionality into IBM Cloud and VPC networking services|
| | Migrate/Redeploy customer IP addressing scheme within the IBM Cloud environment |
| | Provide network isolation with the ability to segregate applications based on attributes such as data classification, public vs internal apps and function  |
| Security | Provide data encryption in transit and at rest|
| | Migrate customer IDS/IAM Services to target IBM Cloud environment |
| | Retain the same firewall rulesets across existing DCs |
| | Firewalls must be restrictively configured to provide advanced security features and prevent all traffic, both inbound and outbound, except that which is specifically required, documented, and approved, and include IPS/IDS services |
| Resiliency | Multi-site capability to support a disaster recovery strategy and solution leveraging IBM Cloud infrastructure DR capabilities|
| | Provide backups for data retention|
| | RTO/RPO = 4 hours/15 minutes; Rollback to original environments should occur no later than specified RTOs |
| | 99.95 Availability|
| | Backups |
| | - Prod: Daily Full, logs per SAP product standard, 30 days retention time \n - Non-Prod: Weekly full, logs per SAP product standard, 14 days retention time|
| Service management | Provide Health and System Monitoring with ability to monitor and correlate performance metrics and events and provide alerting across applications and infrastructure |
| | Ability to diagnose issues and exceptions and identify error sources|
| | Automate management processes to keep applications and infrastructure secure, up to date, and available |
| Other| Migrate SAP workloads from existing data center to IBM Cloud VPC |
| | Customer's SAP systems and applications run on NetWeaver (application) & HANA (DB), AnyDB or S/4 HANA |
| | Provide an Image Replication migration solution that will minimize disruption during cut-over|
| | Cloud infrastructure for the proposed IAAS solution must be SAP Certified |
| | IBM Cloud IaaS will be deployed to support SAP and surrounding non-SAP workloads |
| | Customer does not want to adopt [RISE](https://www.ibm.com/consulting/rise-with-sap?utm_content=SRCWW&p1=Search&p4=43700077624079785&p5=e&gclid=EAIaIQobChMIr9bRlt7LgQMVJdHCBB0cewwcEAAYASAAEgIVgfD_BwE&gclsrc=aw.ds) at this time but wants to consider Cloud deployment solution that would facilitate a future RISE transformation|
{: caption="Table 1. Pattern requirements" caption-side="bottom"}  <!-- each table MUST have a caption attribute>

## Components <!-- H2 -->
{: #components}

<!-- insert the components list, below is an example -->

| Aspect| Component| How the component is used|
|-------------------|--------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------|
| Compute|[VPC VSIs](docs/vpc?topic=vpc-vsi_best_practices&interface=ui)|NetWeaver and HANA DB|
|Storage|[VPC Block Storage](/docs/openshift?topic=openshift-vpc-block)|NetWeaver and HANA DB servers primary storage. Backup storage|
| |[Cloud Object Storage](/docs/cloud-object-storage?topic=cloud-object-storage-about-cloud-object-storage)|Backup and archive, application logs, operational logs and audit logs
|Networking|[VPC Virtual Private Network (VPN)](/docs/iaas-vpn?topic=iaas-vpn-getting-started)|Remote access to manage resources in private network|
| |[Virtual Private Gateway & Virtual Private Endpoint (VPE)](/docs/vpc?topic=vpc-about-vpe)| For private network access to Cloud Services, e.g. Key Protect, COS, etc.|
| | [VPC Load Balancers](/docs/vpc?topic=vpc-load-balancers) | Application Load Balancing for web servers, app servers, and database servers|
| | Public gateway| For web server access to the internet|
| | [Cloud Internet Services (CIS)](/docs/cis?topic=cis-getting-started) | Public Load balancing and DDoS of web servers traffic across zones in the region|
| | [DNS Services](/docs/dns-svcs?topic=dns-svcs-about-dns-services) | |
| | [VPCs and subnets](/docs/vpc?topic=vpc-about-subnets-vpc&interface=ui) | Network Segmentation/Isolation |
| | [Transit Gateway](/docs/transit-gateway?topic=transit-gateway-about) | Connect across multiple VPCs |
| | [IBM Cloud Application Load Balancer](/docs/vpc?topic=vpc-load-balancers-about) (ALB) \n SAP Web Dispatcher | Load balancing workloads across multiple workload instances over the private network |
|Security |[Block Storage encryption](/docs/vpc?topic=vpc-mng-data&interface=ui) with provider keys | Block Storage Encryption at rest |
| | Cloud Object Storage Encryption | Cloud Object Storage Encryption at rest|
| | HANA Data Volume Encryption (DVE) | HANA Database Encryption at rest |
| | [IAM](/docs/account?topic=account-cloudaccess) | IBM Cloud Identity & Access Management |
| | Privileged Identity and Access Management | BYO Bastion host (or Privileged Access Gateway) with PAM SW deployed in Edge VPC |
| | [BYO Bastion Host on VPC VSI with PAM SW](/docs/framework-financial-services?topic=framework-financial-services-vpc-architecture-connectivity-bastion-tutorial-teleport) | Remote access with Privileged Access Management|
| | [Virtual Private Clouds (VPCs), Subnets, Security Groups, ACLs](/docs/vpc?topic=vpc-getting-started) | Core Network Protection|
| | [Cloud Internet Services (CIS)](/docs/cis?topic=cis-getting-started) | DDoS protection and Web App Firewall |
| | One of the following: \n - [Fortigate](https://cloud.ibm.com/catalog/content/ibm-fortigate-AP-HA-terraform-deploy-5dd3e4ba-c94b-43ab-b416-c1c313479cec-global) \n - [Juniper vSRX](https://cloud.ibm.com/catalog/content/juniper-vsrx-catalog-deploy-1.4-dc1e707c-33dd-4321-b2a5-c22dbf0dd0ee-global) \n -[Palo Alto](https://cloud.ibm.com/catalog/content/ibmcloud-vmseries-1.9-6470816d-562d-4627-86a5-fe3ad4e94b30-global)| - IPS/IDS protection at all ingress/egress \n- Unified Threat Management (UTM) Firewall|
| Resiliency | HANA System Replication (HSR) | Provide 99.95% availability for HANA DB|
| | [Veeam](/docs/vpc?topic=vpc-about-veeam) | Controls both the backups and restores of all VSIs or BMs. Veeam Backup & Replication 12 |
| Service Management (Observability) | [IBM Cloud Monitoring](/docs/monitoring?topic=monitoring-about-monitor)| Apps and operational monitoring|
| | [IBM Log Analysis](/docs/log-analysis?topic=log-analysis-getting-started) | Apps and operational logs |
{: caption="Table 2. Pattern components" caption-side="bottom"} <!-- each table MUST have a caption attribute>

As mentioned earlier, the Architecture Framework is used to guide and determine the applicable aspects and domains for which architecture decisions need to be made. The following sections contain the considerations, and architecture decisions for the aspects and domains that are in play in this solution pattern.
