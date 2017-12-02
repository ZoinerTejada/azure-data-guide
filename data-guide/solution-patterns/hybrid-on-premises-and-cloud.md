# Hybrid On-Premises and Cloud Solutions

[About]()  
[When to use this data architecture](#whentouse)  
[Benefits](#benefits)  
[Challenges](#challenges)  
[Hybrid in Azure](#inazure)   
[Where to go from here](#wheretogo)  

<a name="about"></a>
There has been an upward trend for the past several years of business moving to the cloud. The reasons are numerous, given the benefits cloud architectures bring, such as eliminating the need to procure and maintain physical servers, taking advantage of the latest innovations unique to the cloud, and virtually endless scalability of your solutions. But on-premises datacenters also have an important role to play, both today and in the future. For many
organizations, integrating these two to create a hybrid cloud is essential.

To achieve a hybrid cloud, you need a way to connect your on-premises datacenters with the cloud. But basic connectivity isn’t enough; a hybrid cloud should go beyond this, providing a complete set of consistent services. You need access to a broad range of cloud and on-premises technologies that work together in a coherent way.

There are four components of a true hybrid cloud, each of which brings significant benefits. They are the following:

* Common identity for on-premises and cloud applications. This improves user productivity by giving your users single sign-on to all of their applications.
* Integrated management and security across your hybrid cloud. This enables a cohesive way to monitor, manage, and help secure your environment, giving you increased visibility and control.
* A consistent data platform for your datacenter and the cloud. This gives you data portability, combined with seamless access to on-premises and cloud data services for deep insight into your data.
* Unified development and DevOps across the cloud and your on-premises datacenters. This lets you move applications between the two environments as needed, and it also improves developer productivity, since both places now have the same development environment.

Taken together, these four requirements provide consistent experiences for data professionals, developers, IT managers, and users. Because you'll have information both in the cloud and on-premises, it makes sense to have a common approach to working with data in both places. This consistency lets your  use the same tools and skills throughout your environment.

![The four consistent components of a hybrid cloud, provided by Azure](./images/hybrid-cloud.png)

In this guide, we will focus on the consistent data platform for your datacenter and the cloud.

### Network Shares

TODO

### On-premise Data Stores

TODO

### Extending Data Stores to the Cloud

TODO

## <a name="whentouse"></a>When to use this architecture

TODO

## <a name="benefits"></a>Benefits

Using a hybrid on-premises and cloud solution offers the following benefits:

* TODO

## <a name="challenges"></a>Challenges

Establishing a hybrid architecture can surface some of the following challenges:

* TODO

## <a name="inazure"></a>Hybrid in Azure

TODO

New hybrid data integration capabilities in Azure Data Factory including the ability to run SSIS packages within the service. This means you can run your SSIS data integration workloads in Azure, without changing the packages – for true hybrid data integration across on-premises and cloud. And our SSIS partner technologies like Biml can now work to automate and enhance data integration across on-premises and cloud.

![Hybrid on-premises and Azure cloud solution](./images/hybrid-on-premises-cloud.png)

[Azure Stack](https://docs.microsoft.com/azure/azure-stack/)

Some organizations plan to remain hybrid indefinitely. Others, though, view hybrid as a waystation on their journey to the cloud. In other words, they think of a hybrid cloud as part of their migration strategy.

If you're in this second category, a consistent hybrid cloud can make migration significantly easier. For example, Azure Site Recovery can help with migration as well as disaster recovery because it can create new instances of on-premises applications on Azure. Rather than manually moving applications to the cloud, you can rely on Azure Site Recovery to do this and to help you cut over to the new cloud instances. The Microsoft hybrid cloud provides other tools as well, such as the migration wizard built into SQL Server Management Studio to help move on-premises
SQL Server applications to Azure IaaS virtual machines.

Microsoft also helps lower the cost of migration by enabling you to bring your on-premises licenses to Azure. You can use your existing Windows Server licenses with Software Assurance to enable up to 40 percent savings on Windows Server virtual machines in Azure by using the Azure Hybrid Use Benefit. Similarly, license mobility provides the flexibility to deploy existing SQL Server licenses with Software Assurance in the cloud without additional fees. These benefits used alone or together can unlock significant savings as you look to extend into cloud or lift and
shift to cloud. You can also rely on Microsoft’s extensive partner ecosystem, including firms such as Cloudamize and Movere, to provide both migration knowledge and tools.

Whatever options you choose, Microsoft’s consistent approach to hybrid cloud can make migration to a full cloud environment simpler, faster, and less expensive.


## <a name="wheretogo"></a>Where to go from here
Read Next:
[Data ingest technology choices](../technology-choices/data-ingest.md)

See Also:

Related Technology Choices
- [Analysis, Visualizations, & Reporting](../technology-choices/analysis-visualizations-reporting.md)
- [Data Serving Storage](../technology-choices/data-serving-storage.md)
- Real-time Processing