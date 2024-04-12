---

copyright:
  years: 2024
lastupdated: "2024-01-23"

subcollection: <repo-name>

keywords:

---

# Architecture decisions for security
{: #security-architecture}

<!-- below is a placeholder for all compute domain decisions  Remove the domains that are not in scope.  If there are decisions
that need to be added (e.g. platform dependent) add additional rows-->

The following are security architecture decisions for the pattern name.

## Architecture decisions for data security - encryption
{: #data-encryption}

| Architecture decision | Requirement |  Option | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- | -------------- |
| Encryption approach | Encrypt all data to protect it from unauthorized disclosure. | - Encryption with provider keys \n - Encryption with customer-managed keys | text | text |
| Data encryption at rest of primary storage | Encrypt all application data to protect it from unauthorized disclosure. | - Storage encryption with customer-managed keys \n - App-level encryption with customer-managed keys | text | text |
| Data encryption at rest of backups | Encrypt all backup data to protect it from unauthorized disclosure. | text | text | text |
| Data encryption at rest of logs | Encrypt all operational and audit logs at rest to protect them from unauthorized disclosure. | text | text | text |
| Data encryption in transit of web app | Encrypt all application data in transit to protect it from unauthorized disclosure. | Application-level encryption with TLS | Application-level encryption with TLS | Web app uses HTTPS protocol to encrypt data transmissions. |
| Data encryption in transit of DB tier | Encrypt all application data in transit to protect it from unauthorized disclosure. | Application-level encryption with TLS | Application-level encryption with TLS | The database application uses TLS to encrypt data in transit. |
{: caption="Table 1. Data encryption architecture decisions" caption-side="bottom"}

## Architecture decisions for data security - key management
{: #kms}

| Architecture decision | Requirement |  Option | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- | -------------- |
| Key lifecycle management and HSM | Encrypt data at rest and in transit by using customer-managed keys to protect them from unauthorized access.  | Key Protect \n Hyper Protect Crypto Services (HPCS) | Key Protect | Key Protect is recommended for applications that need to comply with regulations requiring encryption of data with customer-managed keys. Key Protect provides key management services by using a shared (multi-tenant) FIPS 140-2 Level 3 certified hardware security modules (HSMs). |
| | | | Hyper Protect Crypto Services (HPCS) | HPCS is recommended for financial services and highly regulated industry applications. HPCS provides Key Management Services with the highest level of security and control that is offered by any cloud provider in the industry. It uses a dedicated (single-tenant) FIPS 140-2 Level 4 certified Hardware Security Module and supports customer-managed master keys, giving the customer exclusive control of the entire key hierarchy. |
| Certificate management | Protect secrets through their entire lifecycle and secure them using access control measures | Secrets Manager \n BYO Certificate Manager | Secrets Manager | IBM Secrets Manager creates, leases, and centrally manages secrets that are used by IBM Cloud Services or customer applications. Secrets are stored in a dedicated instance of Secrets Manager and can be encrypted by using any of IBM Cloud Key Management Services. |
{: caption="Table 2. Key management architecture decisions" caption-side="bottom"}

## Architecture decisions for identity and access management
{: #iam}

| Architecture decision | Requirement |  Option | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- | -------------- |
| Privileged access management        | - Ensure that all operator actions are run securely through a bastion host \n - Implement session recording to track all activities and note any potential threats \n - Manage access to resources and track commands issued | - BYO Bastion Host \n - BYO Bastion Host with Privileged Access Management (PAM) SW                  | BYO Bastion Host with Privileged Access Management (PAM) SW  | The Bastion Host is a Virtual Server instance that is provisioned through SSH over a private network to securely access resources within IBM Cloud’s private network. Using PAM software is recommended to perform session recording and to help track and manage all access.                      |
| Identity access & role management (IDM) | Securely authenticate users for platform services and control access to resources consistently across IBM Cloud| IBM Cloud IAM| IBM Cloud IAM| Use IAM access policies to assign users, service IDs, and trusted profiles access to resources within the IBM Cloud account.|
{: caption="Table 3. Identity and access management architecture decisions" caption-side="bottom"}

## Architecture decisions for application security
{: #app-security}

| Architecture decision | Requirement |  Option | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- | -------------- |
| DDoS | - Enforce information flow policies and protect the boundaries of the application. \n - Protect against or limit the effects of denial-of-service attacks. | IBM Cloud Internet Services (CIS) | IBM Cloud Internet Services (CIS) | IBM Cloud Internet Services provide Distributed Denial of Service (DDoS) to protect applications that are exposed to the public network. |
| Web application firewall | Protect web applications from application layer attacks. | - IBM Cloud Internet Services (CIS) \n - BYO Firewall on Virtual Server for VPC | IBM Cloud Internet Services (CIS) | IBM Cloud Internet Services provides Web Application Firewall security features to protect applications that are exposed to the public network. |
{: caption="Table 4. Application security architecture decisions" caption-side="bottom"}

## Architecture decisions for infrastructure and endpoint
{: #infrastructure and endpoint}

| Architecture decision | Requirement |  Option | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- | -------------- |
| Core network protection                 | -   Strict separation of duties \n-   Isolated security zones between environments \n-   Isolated, private cloud environment| text | text | text |
| Edge and endpoint protection                 | text| text | text | text |
{: caption="Table 5. Infrastructure and endpoint architecture decisions" caption-side="bottom"}

## Architecture decisions for threat detection and response
{: #threat detection and response}

| Architecture decision | Requirement |  Option | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- | -------------- |
|Threat detection and response|- Boundary protection: highest level of isolation from external network threats \n - IPS/IDS protection at all ingress/egress \n - Unified Threat Management (UTM) Firewall|BYO Virtual Firewall (on VSI) in Edge VPC (deployed across availability zones) client choices: \n [Fortigate](https://cloud.ibm.com/catalog/content/ibm-fortigate-AP-HA-terraform-deploy-5dd3e4ba-c94b-43ab-b416-c1c313479cec-global)  \n  [Palo Alto](https://cloud.ibm.com/catalog/content/ibmcloud-vmseries-1.9-6470816d-562d-4627-86a5-fe3ad4e94b30-global)| text |Can be provided by Enterprise Network DMZ \n In addition, if client requires: \n - Virtual FW on VSI in the Transit/Edge VPC \n - Client preference however recommendation is Fortigate or Juniper \n - Fortigate supports native HA configuration \n - Fortigate and Juniper both support both IPS & IDS|
{: caption="Table 6. Threat detection and response architecture decisions" caption-side="bottom"}

## Architecture decisions for governance, risk and compliance
{: #governance, risk and compliance}

| Architecture decision | Requirement |  Option | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- | -------------- |
|Governance, risk and compliance| text | text | text | text|
{: caption="Table 7. Govenrnace, risk and compliance architecture decisions" caption-side="bottom"}
