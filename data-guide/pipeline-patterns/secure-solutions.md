# Secure solutions

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

The first step to protecting information is identifying what to protect. Develop clear, simple, and well-communicated guidelines to identify, protect, and monitor the most important data assets anywhere they reside. This is commonly referred to as Information Security and Data Classification policies. Once identified, establish the strongest protection for assets that have a disproportionate impact on the organization's mission or profitability. These are known as high value assets, or HVAs. Perform stringent analysis of HVA lifecycle and security dependencies, and establish appropriate security controls and conditions. Similarly, identify and classify sensitive assets, and define the technologies and processes to automatically apply security controls.

Once the data you need to protect has been identified, you need to account for the possible states in which your data may occur, and the controls that are available for that state. These data states include:

* At-rest: All information storage objects, containers, and types that exist statically on physical media, whether magnetic or optical disk.
* In-transit: When data is being transferred between components, locations or programs, such as over the network, across a service bus (from on-premises to cloud and vice-versa, including hybrid connections such as ExpressRoute), or during an input/output process, it is thought of as being in-motion.

Learn more about how to protect your data at-rest or in-transit by reading [Azure Data Security and Encryption Best Practices](https://docs.microsoft.com/azure/security/azure-security-data-encryption-best-practices).

### Access Control

Central to protecting your data in the cloud is a combination of identity management and access control. Given the variety and type of cloud services (SaaS, PaaS, and IaaS), as well as the rising popularity of [hybrid cloud](../pipeline-patterns/hybrid-on-premises-and-cloud.md), there are several key practices you should follow when it comes to identity and access control:

* Centralize your identity management
* Enable Single Sign-On (SSO)
* Deploy password management
* Enforce multi-factor authentication (MFA) for users
* Use role based access control (RBAC)
* Conditional Access Policies should be configured, which enhances the classic concept of user identity with additional properties related to user location, device type, patch level, etc.
* Control locations where resources are created using resource manager
* Guide developers to leverage identity capabilities for SaaS apps
* Actively monitor for suspicious activities

Learn more about [Azure Identity Management and access control security best practices](https://docs.microsoft.com/azure/security/azure-security-identity-management-best-practices).

### Auditing

Beyond the identity and access monitoring previously mentioned, the services and applications that you use in the cloud should be generating security-related events that you can monitor. A combination of [monitoring these events and creating alerts](../pipeline-patterns/monitoring-data-solutions.md) for them are important components in an effective data protection strategy.

The primary challenge to monitoring these events is in handling the vast quantities of logs one must evaluate and analyze to stave off potential problems or troubleshoot past ones. Cloud-based applications tend to contain many moving parts, most of which generate some level of logging and telemetry. Your best bet is to use centralized monitoring and analysis to help you manage and make sense of the large amount of information.

Get to know the various types of logs provided by your cloud platform, as well as the monitoring solutions it provides. This can make the difference between proactively dealing with security threats and scrambling trying to put out fires.

Learn more about [logging and auditing in Azure](https://docs.microsoft.com/azure/security/azure-log-audit).

## <a name="whentouse"></a>When to use this architecture

Security should be part of your plan from the beginning of your project lifecycle. For many, the security capabilities a cloud provider offers is the first indicator of its viability for their solution.

## <a name="benefits"></a>Benefits

Using a secure solution offers the following benefits:

* Protect your data from both external and internal threats.
* Gain insight on how your data is being accessed and used.
* Adhere to security and auditing regulations to maintain compliancy within your industry.
* Protect your users' important information; gain and maintain their trust.
* Proper security monitoring and auditing goes beyond simply keeping your data safe - those practices also help ensure the health and stability of your applications in the cloud.

## <a name="challenges"></a>Challenges

Establishing a secure solution can cause you to face some of the following challenges:

* Centralizing the monitoring and analysis of security events stored in numerous logs.
* Implementing encryption and authorization management across your applications and services.
* Ensuring that centralized identity management works across all of your solution components, whether on-premises or in the cloud.

## <a name="inazure"></a>Secure solutions in Azure

Starting with data protection, how you secure your data at rest in Azure depends on where you are keeping it. When using Azure to host your virtual machines, you can leverage [Azure Disk Encryption](https://docs.microsoft.com/azure/security/azure-security-disk-encryption) on your Linux or Windows VMs to help protect and safeguard your data stored by encrypting the attached disks. This solution integrates with [Azure Key Vault](https://docs.microsoft.com/azure/key-vault/) to help you safely control and manage the disk-encryption keys and secrets in your key vault subscription. [Azure Storage Service Encryption](https://docs.microsoft.com/azure/storage/common/storage-service-encryption) for data at rest enables Azure Storage to automatically encrypt your data prior to persisting to storage, and decrypts prior to retrieval. The encryption, decryption, and key management are totally transparent to users. You can use a combination of [Client-Side Encryption and Azure Key Vault](https://docs.microsoft.com/azure/storage/common/storage-client-side-encryption) to easily encrypt at the client before sending your data to Azure Storage.

If you are using Azure SQL Database or Azure SQL Data Warehouse, use the [Transparent Data Encryption](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption-azure-sql) (TDE) feature to perform real-time encryption and decryption of your databases, associated backups, and transaction log files without requiring any changes to your applications. Azure SQL Database and SQL Server can also use [Always Encrypted](https://docs.microsoft.com/azure/sql-database/sql-database-always-encrypted-azure-key-vault) to help protect sensitive data at rest on the server, during movement between client and server, and while the data is in use. Like Azure Disk Encryption, you can use Azure Key Vault to store your Always Encrypted encryption keys. With Always Encrypted, data stored in-memory is also encrypted, making it unrecognizable even to the underlying database system.

You can protect other types of files that you use with [Azure Rights Management](https://docs.microsoft.com/information-protection/understand-explore/what-is-azure-rms) (Azure RMS), the protection technology used by [Azure Information Protection](https://docs.microsoft.com/information-protection/understand-explore/what-is-information-protection). This cloud-based service uses encryption, identity, and authorization policies to help secure your files and email, and it works across multiple devices—phones, tablets, and PCs. Information can be protected both within your organization and outside your organization because that protection remains with the data, even when it leaves your organization's boundaries.

To protect your data in transit, start out by always using SSL/TLS protocols when exchanging data across different locations. Sometimes you need to isolate your entire communication channel between your on-premises and cloud infrastructure by using either a virtual private network (VPN) or [ExpressRoute](https://docs.microsoft.com/azure/expressroute/). More information on using VPNs and ExpressRoute can be found in the [Hybrid On-Premises and Cloud Solutions](../pipeline-patterns/hybrid-on-premises-and-cloud.md) article.

If you are interacting with Azure Storage through the Azure Portal, all transactions occur via TLS. [Storage REST API](https://docs.microsoft.com/rest/api/storageservices/Azure-Storage-Services-REST-API-Reference) over TLS can also be used to interact with Azure Storage and Azure SQL Database. Organizations that fail to protect data in transit are more susceptible for man-in-the-middle attacks, eavesdropping and session hijacking. These attacks can be the first step in gaining access to confidential data.

When it comes to identity and access control, Microsoft offers comprehensive solutions you can use across Azure and other services such as Office 365, to help simplify the management of multiple environments and control user access across applications. For instance, [Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) (Azure AD) can help you manage access to numerous Azure services as well as your custom-built applications, while providing active monitoring for suspicious activities. Azure AD can also help you implement [Role-Based Access Control](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) (RBAC) to restrict your users to the exact permissions they need. If you are using Active Directory on-premises, it is possible to [synchronize with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-directory-sync-requirements) to provide your users with a cloud identity based on their on-premises identity. Use [Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/), a two-step verification solution that delivers strong authentication via a range of verification methods, including phone call, text message, or mobile app verification. You may also opt to integrate a number of third-party SaaS applications, such as Salesforce, with Azure AD for single sign-on, making it easier for your users to gain access to your products and services. These features help ensure the _right people_ can access your applications. When you want to have more control over how the right people are accessing your resources under certain conditions, or perhaps even block them from accessing certain apps under other conditions, use Azure Active Directory [conditional access](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal). This capability is configured by setting conditional access policies through a number of condition statements and controls. For example, your policy statement could take the form of: _When contractors are trying to access our cloud apps from networks that are not trusted, then block access_. Finally, [Azure AD Privileged Identity Management](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-privileged-identity-management-configure) can help you manage, control, and monitor your users and what sorts of tasks they are performing with their admin privileges. This is an important step to limiting who in your organization can carry out privileged operations in Azure AD, Azure, Office 365, or SaaS apps, as well as monitor their activities.

Services that support Azure Active Directory authentication can authenticate between one another by enabling [Managed Service Identity](https://docs.microsoft.com/azure/active-directory/msi-overview) (MSI). When MSI is enabled on an Azure service, Azure automatically creates an identity for the service instance in the Azure AD tenant used by your Azure subscription. Once created, the identity can be used to authenticate to any service that supports Azure AD authentication without having any credentials in your code. This makes your code more secure by removing any service credentials that could otherwise appear on developer workstations or get checked into source control.

The Microsoft [Azure Virtual Network service](https://docs.microsoft.com/azure/virtual-network/virtual-network-vnet-plan-design-arm) enables Azure resources to securely communicate with other in a virtual network (VNet). A virtual network is a representation of your own network in the cloud, and is a logical isolation of the Azure cloud dedicated to your subscription. You can connect virtual networks to other virtual networks, or to your on-premises network. Your data residing on Azure VMs and other Azure services that have been added to a VNet can be protected through the use of [network security groups](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg), reducing the number of potential attack vectors. A network security group contains a list of security rules that allow or deny inbound or outbound network traffic based on source or destination IP address, port, and protocol. The new [Virtual Network service endpoints](https://docs.microsoft.com/azure/virtual-network/virtual-network-service-endpoints-overview) feature allows you to add an additional layer of security over your critical Azure service resources, such as [Azure Storage](https://docs.microsoft.com/azure/storage/common/storage-network-security?toc=%2fazure%2fvirtual-network%2ftoc.json) and [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-vnet-service-endpoint-rule-overview?toc=%2fazure%2fvirtual-network%2ftoc.json), by fully removing public internet access to them and allowing traffic only from your virtual network.

Security monitoring and auditing can be centralized with the help of [Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro). This service automatically collects, analyzes, and integrates log data from your Azure resources, the network, and connected partner solutions, like firewall and endpoint protection solutions, to detect real threats and reduce false positives. A list of prioritized security alerts is shown in Security Center along with the information you need to quickly investigate the problem and recommendations for how to remediate an attack. [Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview), part of the [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) (OMS), also provides centralized access to your logs and helps you analyze that data and create custom alerts based on key factors that you define.

For security monitoring on your managed Azure SQL Database instances, you can take advantage of [Azure SQL Database Threat Detection](https://docs.microsoft.com/azure/sql-database/sql-database-threat-detection), a security intelligence feature built into the Azure SQL Database service. Working around the clock to learn, profile and detect anomalous database activities, Azure SQL Database Threat Detection identifies potential threats to the database. Security officers or other designated administrators can receive an immediate notification about suspicious database activities as they occur. Each notification provides details of the suspicious activity and recommends how to further investigate and mitigate the threat.

For information on securing your own application code that runs in the cloud, refer to the [cloud design security patterns](https://docs.microsoft.com/azure/architecture/patterns/category/security) article, and consider following the code security best practices found in the Microsoft [Security Development Lifecycle](https://www.microsoft.com/sdl) (SDL) to minimize
vulnerabilities and their security impact.

## <a name="wheretogo"></a>Where to go from here
Read Next:
- [Monitoring Data Solutions](../pipeline-patterns/monitoring-data-solutions.md)

See Also:

Related Technology Choices
- [Online Transaction Processing (OLTP) data stores](../technology-choices/oltp-data-stores.md)
- [Pipeline Orchestration, Control Flow, and Data Movement](../technology-choices/pipeline-orchestration-data-movement.md)
- [Data Serving Storage](../technology-choices/data-serving-storage.md)
- [Data Transfer](../technology-choices/data-transfer.md)
- [Data Ingest](../technology-choices/data-ingest.md)