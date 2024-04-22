---
copyright:
  years: 2024
lastupdated: "2024-04-11"

subcollection: pattern-webapp-openshift-vpc

keywords:
---
# Architecture decisions for resiliency

The following are resiliency architecture decisions for the Red Hat OpenShift on VPC cluster design.

| **Architecture decision** | **Requirement**                                                                                        | **Alternative**                                                                                                                                                                                                                                                                      | **Decision**                          | **Rationale**                                                                                                                                                                                                                                                                                                                     |
| ------------------------------- | ------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| High Availability               | -Ensure availability of resources in the event of outages.  Support SLA targets for application availability | -[Single-zone cluster](https://cloud.ibm.com/docs/openshift?topic=openshift-ha_clusters) - [Multi-zone cluster](https://cloud.ibm.com/docs/openshift?topic=openshift-ha_clusters) - [Multiple single-zone clusters in one region](https://cloud.ibm.com/docs/openshift?topic=openshift-ha_clusters) | - Multizone clusters (3 availability zones) | - Built-in high availability leveraging 3 availability zones within a region protects against zone failures. - Minimum of 2 worker nodes on each zone (total of 6 worker nodes) required to meet IBM Cloud 99.99% SLA. - Each zone configured with 50% of required CPU capacity to provide 100% capacity in the event of a zone failure |
