---
copyright:
  years: 2024
lastupdated: "2024-04-12"

subcollection: pattern-webapp-openshift-vp

keywords:
---
{{site.data.keyword.attribute-definition-list}}

# Overview

{: #overview}

This Red Hat OpenShift on IBM Cloud VPC pattern provides a solution design for microservices based architecture, for an E-commerce environment. This is specifically based on one in use today by HomeDIY Ltd, who are growing their online presence rapidly and have standardised on IBM Cloud for their new modern architecture.
This pattern considers 2 channels for the E-commerce solution:  Mobile Application and Website

The application should be built using a future-proof architecture that can adapt to changing technology trends and business needs over time. This includes using modular design principles, microservices architecture, and containerization technologies.
The application should be able to scale up or down as per the traffic demand without any downtime or performance degradation. It should also have high availability features to minimize downtime due to server failures or maintenance activities.
The application should have robust security features to protect sensitive customer data, including personal details. This includes implementing secure protocols for data transfer, such as HTTPS, and using encryption techniques to protect data at rest and in transit.
The application should have an intuitive and user-friendly interface that makes it easy for customers to navigate and find what they are looking for. This includes features like clear product categorization, relevant search filters, and a clean, modern design.
The application should be mobile-responsive, meaning it should adapt to different screen sizes and orientations, providing an optimal user experience on smartphones and tablets.
The application should have fast page loads to ensure a smooth customer experience. This can be achieved by optimizing images, minifying code, and using caching techniques.

**Assumed Baselines**

**Mobile application**

20000 users, average workload 1000 API transactions per second, message volumetrics/size. Year on year growth is estimated at 15%.

**Web application**

15000 users, average workload 750 API transactions per second, message volumetrics/size. Year on year growth is estimated at 15%

The 20 Node.js microservices will include the following E-commerce components:

- API Gateway services
- Mobile shopping
- Web shopping
- Identity microservices
- Catalog microservices
- Ordering microservice
- Marketing and Recommendations microservice
- Marketplace microservice
- Message bus/orchestration service
- Shopping cart microservice

**Objectives**

This pattern will provide guidance on the following topics:

- Worker node and cluster sizing for the given use case stateful workload requirements.
- Microservice deployment within a cluster.
- Custer capacity planning and optimization.
- Resiliency within a multi-zone VPC region.
- Service management options and considerations.
- Network Isolation: Segregation of workloads through network policies, preventing unauthorized access and securing communication between pods or workloads.
- Encrypted Communication: Utilizes TLS encryption for inter-pod communication, ensuring data confidentiality and integrity within the cluster.
- Access Control: Implements role-based access control (RBAC) to regulate user permissions, limiting unauthorized access and bolstering security posture.
- Traffic Management: Efficiently manages network traffic flow, enabling load balancing and traffic routing for optimal performance and resilience.
- Firewall Protection: Implements firewall rules and network policies to restrict incoming and outgoing traffic, fortifying the cluster against potential threats.
- Intrusion Detection and Prevention: Incorporates monitoring tools to detect and prevent suspicious activities, mitigating potential security breaches proactively.

The Red Hat OpenShift on IBM Cloud VPC pattern is intended to:

- Accelerate and simplify solution design by providing a standard IBM Cloud deployment architecture reference following the [IBM Architecture Framework](https://cloud.ibm.com/docs/architecture-framework).
- Provide a prescriptive, end-2-end enterprise-class solution design, with diagrams, component architecture decisions along with rationale for cloud component selection to meet enterprise requirements.
- Ensure requirements can be met from a performance, security and compliance, availability, and observability perspective.


The Architecture Framework provides a consistent approach to design cloud solutions by addressing requirements across a set of "aspects" and "domains", which are technology-agnostic architectural areas that need to be considered for any enterprise solution. For more details, see [Introduction to the Architecture Framework](/docs/architecture-framework).
