# Secure Solutions

[About]()  
[When to use this data architecture](#whentouse)  
[Benefits](#benefits)  
[Challenges](#challenges)  
[Secure solutions in Azure](#inazure)   
[Where to go from here](#wheretogo)  

<a name="about"></a>
For many, making data accessible in the cloud, particularly when transitioning from working exclusively in on-premises data stores, can cause some concern around increased accessibility to that data and new ways in which to secure it.

Security in the cloud is a partnership between you and your cloud provider. Your cloud provider provides you security controls and capabilities to help you protect your data and applications, while you own your data and identities and the responsibility for protecting them, the security of your on-premises resources, and the security of cloud components you control.

The responsibilities and controls for the security of applications and networks vary by the service type:

* **Software as a Service (SaaS)**: Your cloud provider operates and secures the infrastructure, host operating system, and application layers. Data is secured at datacenters and in transit between you and the cloud. You control access and secure your data and identities, including configuring the set of application controls available in the cloud service.
* **Platform as a Service (PaaS)**: Your cloud provider operates and secures the infrastructure and host operating system layers. You control access and secure your data, identities, and applications, including applying any infrastructure controls available from the cloud service. You also control all application code and configuration.
* **Infrastructure as a Service (IaaS)**: Your cloud provider operates and secures the base infrastructure and host operating system layers. You control access and secure data, identities, applications, virtualized operating systems, and any infrastructure controls available from the cloud service.

Learn more about these topics in [Security in a Cloud-Enabled World](https://mva.microsoft.com/training-courses/security-in-a-cloudenabled-world-12725?l=CfLHobAcB_3904300474), provided by Microsoft Virtual Academy.

### Data Protection

The first step to protecting information is identifying what to protect. Develop clear, simple, and well-communicated guidelines to identify, protect, and monitor the most important data assets anywhere they reside. Once identified, establish the strongest protection for assets that have a disproportionate impact on the organization's mission or profitability. These are known as high value assets, or HVAs. Perform stringent analysis of HVA lifecycle and security dependencies, and establish appropriate security controls and conditions. Similarly, identify and classify sensitive assets, and define the technologies and processes to automatically apply security controls.

Once the data you need to protect has been identified, you need to account for the possible states in which your data may occur, and the controls that are available for that state. These data states include:

* At-rest: All information storage objects, containers, and types that exist statically on physical media, whether magnetic or optical disk.
* In-transit: When data is being transferred between components, locations or programs, such as over the network, across a service bus (from on-premises to cloud and vice-versa, including hybrid connections such as ExpressRoute), or during an input/output process, it is thought of as being in-motion.

Learn more about how to protect your data at-rest or in-transit by reading [Azure Data Security and Encryption Best Practices](https://docs.microsoft.com/azure/security/azure-security-data-encryption-best-practices).

### Access Control

Central to protecting your data in the cloud is a combination of identity management and access control. Given the variety and type of cloud services (SaaS, PaaS, and IaaS), as well as the rising popularity of [hybrid cloud](../solution-patterns/hybrid-on-premises-and-cloud.md), there are several key practices you should follow when it comes to identity and access control:

* Centralize your identity management
* Enable Single Sign-On (SSO)
* Deploy password management
* Enforce multi-factor authentication (MFA) for users
* Use role based access control (RBAC)
* Control locations where resources are created using resource manager
* Guide developers to leverage identity capabilities for SaaS apps
* Actively monitor for suspicious activities

Learn more about [Azure Identity Management and access control security best practices](https://docs.microsoft.com/azure/security/azure-security-identity-management-best-practices).

### Auditing

TODO

## <a name="whentouse"></a>When to use this architecture

TODO

## <a name="benefits"></a>Benefits

Using a secure solution offers the following benefits:

* TODO

## <a name="challenges"></a>Challenges

Establishing a secure solution can surface some of the following challenges:

* TODO

## <a name="inazure"></a>Secure solutions in Azure

TODO

OMS Security and Auditing (Security Threat Analysis)
[Azure Rights Management](https://docs.microsoft.com/information-protection/understand-explore/what-is-azure-rms) (RMS)
Security Development Lifecycle (SDL)
Azure Key Vault
Azure Active Directory and Multi-Factor Authentication
Third-party SaaS identity management

## <a name="wheretogo"></a>Where to go from here
Read Next:
[Pipeline Orchestration, Control Flow, and Data Movement technology choices](../technology-choices/pipeline-orchestration-data-movement.md)

See Also:

Related Solution Patterns
- [Monitoring Data Solutions](../solution-patterns/monitoring-data-solutions.md)

Related Technology Choices
- [Online Transaction Processing (OLTP) data stores](../technology-choices/oltp-data-stores.md)
- [Data Serving Storage](../technology-choices/data-serving-storage.md)
- [Data Transfer](../technology-choices/data-transfer.md)
- [Data Ingest](../technology-choices/data-ingest.md)