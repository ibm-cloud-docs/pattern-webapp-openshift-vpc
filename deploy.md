---
copyright:
  years: 2024
lastupdated: "2024-08-22"

subcollection: pattern-openshift-vpc-mz-resiliency

keywords:
---
{{site.data.keyword.attribute-definition-list}}

# Deploying an OpenShift VPC multi zone architecture

{: #ROKS-vpc--mz-da}

This guide outlines deploying a single region Red Hat OpenShift architecture in a multi zone resilient configuratio, specifically in thre availability zones. The deployment is based on an existing deployable architecture template, as well as a series of customizations to tailor the setup to the specific requirements for your environment.

This is designed for customers who need a scalable, multi-zone kubernetes infrastructure with the flexibility of customizations post the initial deployment of the base Deployable Architecture. It allows for adapting various components, such as networking and security, to better suit individual business needs after the foundational architecture has been established.

## Before you begin
{: #ROKS-vpc-mz-prereqs}

You need the following items to deploy and configure this reference architecture:

* An [IBM Cloud account](https://cloud.ibm.com/registration).
* [Required IAM access policies](https://github.com/terraform-ibm-modules/terraform-ibm-web-app-mzr-da/tree/main/solutions/e2e#required-iam-access-policies).
* A VPC [public and private SSH key pair](https://cloud.ibm.com/docs/vpc?topic=vpc-ssh-keys&interface=ui) that is not in the deployment region.
* An [IBM Cloud API key](https://cloud.ibm.com/docs/account?topic=account-userapikey&interface=ui) for the user or service ID with the correct IAM access policies.
* Review [Planning for the landing zone deployable architectures](https://cloud.ibm.com/docs/secure-infrastructure-vpc?topic=secure-infrastructure-vpc-plan).

## Provision Architecture
{: #provision-vpc-vsi-cross}

1. Select two [VPC multi-zone region](https://cloud.ibm.com/docs/vpc?topic=vpc-creating-a-vpc-in-a-different-region&interface=cli) that you will provision in.
2. Provision the [Web App Multi-Zone Resiliency Deployable Architecture](https://cloud.ibm.com/catalog/7a4d68b4-cf8b-40cd-a3d1-f49aff526eb3/architecture/deploy-arch-ibm-web-app-mzr-75982e34-7b50-4945-96d9-4f686d669fc9-global) in the first region that you chose.
3. Provision the [Web App Multi-Zone Resiliency Deployable Architecture](https://cloud.ibm.com/catalog/7a4d68b4-cf8b-40cd-a3d1-f49aff526eb3/architecture/deploy-arch-ibm-web-app-mzr-75982e34-7b50-4945-96d9-4f686d669fc9-global) in the second region that you chose.  You will need to update the the [subnets within the override.tftpl](https://github.com/terraform-ibm-modules/terraform-ibm-web-app-mzr-da/blob/main/solutions/e2e/override.tftpl) and provide different CIDR blocks so they do not overlap the first deployment.
4. Create a [cross-region IBM Cloud Transit Gateway](https://cloud.ibm.com/docs/transit-gateway?topic=transit-gateway-ordering-transit-gateway&interface=ui) between the workload VPC of the deployed architectures.

## Additonal Services
{: #additonal-srv-vpc-vsi-cross}

You can add additional services onto the 3-tier web application.  The addtional services include:

1. [Account Infrastructure base](https://cloud.ibm.com/catalog/7a4d68b4-cf8b-40cd-a3d1-f49aff526eb3/architecture/deploy-arch-ibm-account-infra-base-63641cec-6093-4b4f-b7b0-98d2f4185cd6-global) for creating and configuring the foundational components of an IBM Cloud account
2. [IBM Cloud Observability](https://cloud.ibm.com/catalog/7a4d68b4-cf8b-40cd-a3d1-f49aff526eb3/architecture/deploy-arch-ibm-observability-a3137d28-79e0-479d-8a24-758ebd5a0eab-global) for provisioning and configuring logging, monitoring, and activity tracking.
3. [IBM Cloud Event Notifications](https://cloud.ibm.com/catalog/7a4d68b4-cf8b-40cd-a3d1-f49aff526eb3/architecture/deploy-arch-ibm-event-notifications-c7ac3ee6-4f48-4236-b974-b0cd8c624a46-global) for a high-throughput message bus that is built with Apache Kafka.
4. [Security and Compliance Center](https://cloud.ibm.com/catalog/7a4d68b4-cf8b-40cd-a3d1-f49aff526eb3/architecture/deploy-arch-ibm-scc-9423f9bc-1290-4c71-a9ac-01898bfa7ccc-global) for compliance posture of your deployed resources.
5. [IBM Cloud Internet Services](https://github.com/terraform-ibm-modules/terraform-ibm-cis) powered by Cloudflare, provides a fast, highly performant, reliable, and secure internet service.
6. [IBM Storage Protect](https://cloud.ibm.com/catalog/content/SPonIBMCloud-20c54034-d319-48c0-beb6-0b4adc54265c-global?catalog_query=aHR0cHM6Ly9jbG91ZC5pYm0uY29tL2NhdGFsb2c%2Fc2VhcmNoPXN0b3JhZ2UlMjUyMHByb3RlY3Qjc2VhcmNoX3Jlc3VsdHM%3D) for data protection operations.
