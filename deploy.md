---
copyright:
  years: 2024
lastupdated: "2024-10-01"

subcollection: pattern-webapp-openshift-vpc

keywords:
---
{{site.data.keyword.attribute-definition-list}}

# Deploying a Red Hat OpenShift VPC multizone architecture
{: #roks-vpc--mz-da}

This guide outlines deploying a single region Red Hat OpenShift architecture in a multizone resilient configuration, specifically in three availability zones. The deployment is based on an existing deployable architecture template, as well as a series of customizations to tailor the setup to the specific requirements for your environment.

This is designed for customers who need a scalable, multizone Kubernetes infrastructure with the flexibility of customizations after the initial deployment of the base deployable architecture. It allows for adapting various components, such as networking and security, to better suit individual business needs after the foundational architecture has been established.

## Before you begin
{: #roks-vpc-mz-prereqs}

You need the following items to deploy and configure this reference architecture:

* An [IBM Cloud account](https://cloud.ibm.com/registration){: external}.
* [Required IAM access policies](https://github.com/terraform-ibm-modules/terraform-ibm-web-app-mzr-da/tree/main/solutions/e2e#required-iam-access-policies).
* A VPC [public and private SSH key pair](/docs/vpc?topic=vpc-ssh-keys&interface=ui) that is not in the deployment region.
* An [IBM Cloud API key](/docs/account?topic=account-userapikey&interface=ui) for the user or service ID with the correct IAM access policies.
* An understanding of the [Planning for the landing zone deployable architectures](/docs/secure-infrastructure-vpc?topic=secure-infrastructure-vpc-plan).

## Provisioning the architecture
{: #provision-roks-vpc-mz}

1. Select the [VPC multi-zone region](/docs/vpc?topic=vpc-creating-a-vpc-in-a-different-region&interface=cli) that you want to provision in.
2. Provision the [Red Hat Openshift VPC Multizone Deployable architecture](https://cloud.ibm.com/docs/deployable-reference-architectures?topic=deployable-reference-architectures-ocp-ra){: external} 
3. Add required and optional parameters
4. Provision a VSI within a subnet on the Red Hat Openshift landing zone using the the [VSI extension Deployable architecture](/docs/secure-infrastructure-vpc?topic=secure-infrastructure-vpc-vsi-ext-ra)
5. Add required and optional parameters and deploy.

For the Openshift deployable architecture the following parameters need to be set:

* Required tab: `api_key` (can be connected to Secrets Manager instance to input)
* Required tab: `region` and `prefix`
* Optional tab: `vpcs` (set to just workload)

For the VSI Extension deployable architecture the following parameters need to be set:

* Required tab: `ssh_public_key`, `region`, `boot_volume_encryption_key`(use crn from kms instance in ROKS DA), `vpc_id`(from ROKS DA)
* Optional tab: `subnet_names`(to avoid 1 vsi every subnet specify the names of a subnet across the three zones ie; vsi-zone-1, vsi-zone-2, vsi-zone-3)

For access to Openshift UI provision a [VPN](https://cloud.ibm.com/docs/vpc?topic=vpc-vpn-create-server&interface=ui)


## Post install options
{: #provision-vsi-bastion-host-software}
To install and configure the bastion host software on a virtual server instance follow the [Bastion software install guide](/docs/solution-tutorials?topic=solution-tutorials-vpc-secure-management-bastion-server)


{: #provision-portworx-software-defined-storage}

1. Follow the [Portworx prerequisites](https://docs.portworx.com/portworx-enterprise/platform/kubernetes/ibm-iks/before-you-begin)
2. Follow the [Portworx deployment guide](/docs/openshift?topic=openshift-storage_portworx_deploy)
   
{: #provision-a-privileged-access-gateway}
This is an alternative approach to configuring a bastion host on a VSI. Follow the [Priviliged Access Gateway deployment guide](/docs/allowlist/privileged-access-gateway?topic=privileged-access-gateway-pag-prep-vsi)

## Additional services
{: #additonal-roks-vpx-mz-services}

You can add additional services onto the 3-tier web application. The additional services include:

1. [IBM Cloud Observability](https://cloud.ibm.com/catalog/7a4d68b4-cf8b-40cd-a3d1-f49aff526eb3/architecture/deploy-arch-ibm-observability-a3137d28-79e0-479d-8a24-758ebd5a0eab-global){: external} for provisioning and configuring logging, monitoring, and activity tracking.
2. [IBM Cloud Event Notifications](https://cloud.ibm.com/catalog/7a4d68b4-cf8b-40cd-a3d1-f49aff526eb3/architecture/deploy-arch-ibm-event-notifications-c7ac3ee6-4f48-4236-b974-b0cd8c624a46-global){: external} for a high-throughput message bus that is built with Apache Kafka.
3. [Security and Compliance Center](https://cloud.ibm.com/catalog/7a4d68b4-cf8b-40cd-a3d1-f49aff526eb3/architecture/deploy-arch-ibm-scc-9423f9bc-1290-4c71-a9ac-01898bfa7ccc-global){: external} for compliance posture of your deployed resources.
4. [IBM Cloud Internet Services](https://github.com/terraform-ibm-modules/terraform-ibm-cis){: external} powered by Cloudflare, provides a fast, highly performant, reliable, and secure internet service.
5. [IBM Storage Protect](https://cloud.ibm.com/catalog/content/SPonIBMCloud-20c54034-d319-48c0-beb6-0b4adc54265c-global?catalog_query=aHR0cHM6Ly9jbG91ZC5pYm0uY29tL2NhdGFsb2c%2Fc2VhcmNoPXN0b3JhZ2UlMjUyMHByb3RlY3Qjc2VhcmNoX3Jlc3VsdHM%3D){: external} for data protection operations.
