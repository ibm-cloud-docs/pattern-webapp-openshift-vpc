---
copyright:
  years: 2024
lastupdated: "2024-04-11"

subcollection: pattern-webapp-openshift-vpc

keywords:
---
{{site.data.keyword.attribute-definition-list}}

# Security design
{: #security-design}

![A screenshot of a computer Description automatically generated](image/Merged_Reference_OpenShift-security.drawio.svg){: caption="Figure 1. Security design for web application deployment" caption-side="bottom"}

Manage cloud as code is designed to automate everything from application infrastructure to account creation and compliance monitoring.

Separation of environments follows principle of separation of duties and least privilege:

- Separation of duties - No user should be given enough privileges to misuse the system on their own. No developer access to production.
- Least privilege - restrict access privileges of authorized personnel to the minimum necessary to perform their jobs.

separate resource groups to isolate production and non-production environments. Within each resource group a landing zone is created using a VPC.

The Production VPC is privatenot connected to the internet with administrative and operator access through a Bastion host.

VPC access control lists and security groups provide filter and secure traffic to only trusted sources (CIS and ICOS).

Deploy the OpenShift clusters using “[Secure by Default” with zero trust networking model](https://community.ibm.com/community/user/cloud/blogs/cale-rath/2024/03/07/secure-by-default-cluster-networking). Map the IBM Cloud IAM roles to the RBACs [for platform and service roles](https://cloud.ibm.com/docs/openshift?topic=openshift-iam-platform-access-roles&interface=ui).

Consider that image registry is private, highly available, secure and includes vulnerability scanner.

Application, databases, backup, and log data are encrypted at rest by using storage encryption with customer-managed keys through the integration of VPC Block and Cloud Object Storage services with IBM Cloud Key Management Services (KMS).

The web app encrypts data in transit by using TLS encryption. The Secrets Manager cloud service is used to store and manage secrets and credentials to access applications and cloud resources, as well as SSL/TLS certificates and private keys.

Key Protect is used to support data encryption with customer-provided keys to meet regulatory compliance requirements. Key Protect uses a shared FIPS 140-2 level 3 certified hardware security module (HSM) to store keys that are used by storage services for envelope encryption and is also used to offload TLS/SSL keys.

App ID is used to add authentication and authorization for the mobile app connecting users from internet to Web application.
