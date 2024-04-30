---
copyright:
  years: 2024
lastupdated: "2024-04-29"

subcollection: pattern-webapp-openshift-vpc

keywords:
---
# Architecture decisions for resiliency

The following are resiliency architecture decisions for the Red Hat OpenShift on VPC cluster pattern.

| Architecture decision | Requirement                                                                                        | Alternative                                                                                                                                                                                                                                                                      | Decision                          | Rationale                                                                                                                                                                                                                                                                                                                     |
| ------------------------------- | ------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| High availability               | * Ensure availability of resources if there's an outages. Support Service Level Agreement (SLA) targets for application availability | * [Single-zone cluster](/docs/openshift?topic=openshift-ha_clusters)\n * [Multi-zone cluster](/docs/openshift?topic=openshift-ha_clusters) \n * [Multiple single-zone clusters in one region](/docs/openshift?topic=openshift-ha_clusters) | * Multizone clusters: 3 availability zones | * Built-in high availability that uses three availability zones within a region protects against zone failures. \n * Minimum of two worker nodes on each zone for a total of 6 worker nodes is required to meet IBM Cloud 99.99% SLA. \n *  Each zone configured with 50% of required CPU capacity to provide 100% capacity if there's a zone failure. |
{: caption="Table 1. Architecture decisions for resilliency" caption-side="bottom"}
