---
copyright:
  years: 2024
lastupdated: "2024-04-29"

subcollection: pattern-webapp-openshift-vpc

keywords:
---
{{site.data.keyword.attribute-definition-list}}

# Network design
{: #network-design}

![A diagram of a computer description automatically generated](image/Merged_Reference_OpenShift-Networking.drawio.svg){: caption="Figure 1. Network design for web application deployment" caption-side="bottom"}


- HomeDIY commerce system is a web application accessible from web browsers, mobile applications, and other connected apps through IBM Cloud Internet Services (CIS). It acts as a global load balancer with the Content Delivery Network (CDN), Web Application Firewall (WAF), and Distributed Denial of Service (DDoS) capabilities.
- Only HTTPS traffic, Port 443, is allowed through CIS.
- The operations and system admin team that manages this system accesses various environments through a secure Virtual Private Network (VPN) connection that allows SSH-only connection through Port 22.
- For a website request (1), the CIS forwards to the IBM Cloud Object Storage where the static website is hosted.
- For an API request, the CIS forwards to a load balancer
- For a website request, the static web application hosted in IBM Cloud Object Storage propagated in Point of Presence (POP) locations gets served through Content Delivery Network (CDN).
- Ideally, the static web application in IBM Cloud Object Storage is hosted in a public internet-facing network segment as these are the only internet-facing workloads.
- The API request, from static websites and mobile apps(2), reaches the Back End For Frontend (BFF) microservices hosted in Red Hat OpenShift on IBM Cloud Red Hat Openshift cluster deployed in a Virtual Private Cloud (VPC).
- A network load balancer (3) distributes the traffic across the Red Hat Openshift worker nodes spread across the multiple availability zones.
- As per the routes (4) in the Red Hat Openshift cluster, the traffic is then forwarded to the appropriate Kubernetes service which caters to the business logic in a Kubernetes pod as a microservice.
- The business logic written as Back End For Front End (BFF) microservices is the data access layer for the application. They access the backend and handle sensitive user data for the application.
- Ideally, the business logic / BFF deployed in Red Hat Openshift clusters are in a private network segment. Meaning there is no direct internet access is allowed.
- The workloads based on their type can be deployed in the Red Hat Openshift cluster using projects (5)(namespaces). For example, the back-end for frontend microservices can be deployed in a project named “prod-bff-microservices”, in the case of non-production environments the project can be named “dev-bff-microservicss” or “test-bff-microservices”.
- By default, in Red Hat Openshift the communication across the workloads in different projects is open.
- By applying appropriate Kubernetes network policies, communication within the workloads can be allowed or restricted.
- The Red Hat OpenShift service mesh (6) controls service-to-service communication in a microservices architecture. It controls the delivery of service requests to other services, performs load balancing, encrypts data, and discovers other services.
- The connectivity to the other IBM Cloud services is via Virtual Private Endpoints (VPE) (7) within IBM Cloud.
- The production environment is deployed in a separate VPC with appropriate access via Network access control lists (ACLs) and security policies.
- The non-production environments deployed in a different VPC which can only be accessed by internal audiences like developers, testers, and the operations team.
- Deploying the environments in different Red Hat Openshift clusters in different VPCs provides fine-grained segregation between networking, access privilege, and security to each of them.

## Network Considerations
{: #network-considerations}

![A diagram of a computer Description automatically generated](image/Merged_Reference_OpenShift-NetworkingLayers.drawio.svg){: caption="Figure 2. Layers of a web application deployment in cloud" caption-side="bottom"}

The network design for the HomeDIY -commerce application follows a layered approachsegregation of responsibility. These layers help in identifying which workloads need to be public-facing and which need to be considered as secure and deployed in a private zone.

1. Presentation Layer (Public Zone – Internet Facing Workload)
2. Integration Layer (Private Zone – Secure Workload)
3. Services Layer (Private Zone – Secure Workload)
4. Data access Layer (Private Zone – Secure Workload)
5. Data Storage Layer (Private Zone – Secure Workload)

**Public Zone – Internet Facing Workload**
{: #network-public-zone}

In a cloud deployment architecture, a Public Zone is a network segment placed between an organization's internal and external networks, typically the Internet. Its purpose is to provide additional security by isolating internet-facing services and workloads from the internal network, protecting sensitive data and critical systems from potential security threats originating from the internet.

- The HomeDIY -commerce application's internet-facing static content (Presentation Layer) is deployed in IBM Cloud Object Storage.

- Static contents like HTML, JavaScript, and Images/Videos are served from IBM Cloud Object Storage to internet users.

- All requests reaching IBM Cloud Object Storage are via Cloud Internet Services (CIS), which acts as a public/global load balancer with DDoS protection.

- CIS has multiple Point of Presence (PoP) locations for Content Delivery Network (CDN) capability, improving user experience and application performance.

- CDNs cache static content like images, stylesheets, and scripts on their servers, reducing the load on the origin server when users request these resources.

In the Public Zone, organizations can strike a balance between offering external access to internet-facing services while maintaining the security and integrity of internal networks and sensitive data. This is crucial in cloud deployments where scalability and flexibility are essential for adapting to changing workloads and evolving security threats.

In the Public Zone, organizations can maintain a balance between providing external access to internet-facing services and ensuring the security and integrity of their internal networks and sensitive data. This approach is particularly crucial in cloud deployments, where scalable and flexible solutions are essential for adapting to dynamic workloads and evolving security threats.


**Private Zone (Secure Workloads)**
{: #network-private-zone}

In the HomeDIY E-commerce application deployment, business functions, integrations, services, data access, and storage layers are deployed in a private zone, which includes additional security policies and filtered traffic. The Red Hat Openshift cluster is deployed in a VPC with security policies, and all traffic is routed through a VPC Load Balancer to distribute traffic across multiple availability zones. Microservices are exposed to static web apps or mobile apps using Routes objects in Red Hat OpenShift. Network policies define ingress/egress to and from pods or microservices, and Red Hat OpenShift service mesh adds an additional layer of control in Layer 7. The BFF microservices are enrolled in the Red Hat OpenShift service mesh for flexibility in controlling traffic through a sidecar proxy. Workloads in the Red Hat Openshift cluster need access to IBM Cloud services, which can be connected via a Virtual Private Endpoint (VPE ) connection.
