# Online Analytical Processing (OLAP) data stores

[About]()  
[What are your options when choosing an OLAP data store?](#options)  
[How do you choose?](#howtochoose)  
[Key selection criteria](#criteria)  
[Capability matrix](#matrix)   
[Where to go from here](#wheretogo)  

<a name="about"></a>

## <a name="options"></a> What are your options when choosing an OLAP data store?
In Azure, all of the following data stores will meet the core requirements for OLAP:

- [SQL Server with Columnstore indexes](https://docs.microsoft.com/sql/relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics)
- [Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-overview)
- [SQL Server Analysis Services (SSAS)](https://docs.microsoft.com/sql/analysis-services/analysis-services)

SQL Server Analysis Services (SSAS) offers OLAP and data mining functionality for business intelligence applications. You can either install SSAS on local servers, or host within a virtual machine in Azure. Azure Analysis Services is a fully managed platform as a service (PaaS) offering that provides the same major features as SSAS, but in the cloud. Because Azure Analysis Services lives in the cloud, its servers support connecting to [various data sources](https://docs.microsoft.com/azure/analysis-services/analysis-services-datasource) in the cloud and on-premises in your organization.

Clustered Columnstore indexes are available in SQL Server 2014 and above, as well as Azure SQL Database, and are ideal for OLAP workloads. However, beginning with SQL Server 2016 (including Azure SQL Database), you can take advantage of hybrid transactional/analytics processing (HTAP) through the use of updateable nonclustered columnstore indexes. HTAP enables you to perform OLTP and OLAP processing on the same platform, which removes the need to store multiple copies of your data, and eliminates the need for distinct OLTP and OLAP systems. For more information, see [Get started with Columnstore for real-time operational analytics](https://docs.microsoft.com/sql/relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics).

## <a name="howtochoose"></a> How do you choose?
Each data store brings with it a unique set of capabilities, giving you the option to select the one that most closely meets your requirements. 

## <a name="criteria"></a> Key selection criteria

The following tables summarize the key differences in capabilities between each. For OLAP scenarios, choose the appropriate system for your needs by answering these questions:

- Do you want a managed service or do you prefer to manage your own physical or virtual servers?
    - If yes (you want a managed service), then narrow your options to those that are managed services, such as Azure Analysis Services and Azure SQL Database.
- Do you require secure authentication using Azure Active Directory (Azure AD)?
    - If yes, then you will need one of the options that Azure AD integration.
- Do you want to conduct real-time analytics?
    - If so, narrow your options to those that support real-time analytics, such as SQL Server + Columnstore indexes. Real-time operational analytics targets the scenario of a single data source such as an enterprise resource planning (ERP) application on which you can run both the operational and the analytics workload. This does not replace the need for a separate data warehouse when you need to integrate data from multiple sources before you run the analytics workload, or when you require extreme analytics performance by using pre-aggregated data such as cubes.
- Do you need the ability to use pre-aggregated data, such as to provide semantic models that make analytics more business user friendly?
    - If yes, then you will want an option that provides support for multidimensional cubes or tabular semantic models. This is typically preferred when providing aggregates helps business users consistently calculate data aggregates in a way that makes sense for your data. Pre-aggregated data can also provide a large performance boost when dealing with several columns across many rows. Data can be pre-aggregated in multidimensional cubes or tabular semantic models.
- Do you need the ability to integrate data from several sources, beyond your OLTP data store?
    - If so, consider options that easily integrate multiple data sources.

## <a name="matrix"></a> Capability matrix

### General capabilities

| | Azure Analysis Services | SQL Server Analysis Services | SQL Server in Azure Virtual Machine + Columnstore Indexes | Azure SQL Database + Columnstore Indexes |
| --- | --- | --- | --- | --- |
| Is managed service | Yes | No | No | Yes |
| Supports multidimensional cubes | No | Yes | No | No |
| Supports tabular semantic models | Yes | Yes | No | No |
| Easily integrate multiple data sources | Yes | Yes | No \* | No \* |
| Supports real-time analytics | No | No | Yes | Yes |
| Requires process to copy data from source(s) | Yes | Yes | No | No |
| Azure Active Directory (AAD) integration | Yes | No | No \** | Yes |

\* While SQL Server or Azure SQL Database cannot be used to query from and integrate multiple external data sources, you can still build a pipeline that does this for you using [SSIS](https://docs.microsoft.com/sql/integration-services/sql-server-integration-services) or [Azure Data Factory](https://docs.microsoft.com/azure/data-factory/). SQL Server hosted in an Azure VM has additional options, such as linked servers (other SQL Servers, Oracle, etc.) and [PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide). See [Options for Pipeline Orchestration, Control Flow, and Data Movement](../technology-choices/pipeline-orchestration-data-movement.md) for more information.

\** Connecting to SQL Server running on an Azure Virtual Machine is not supported using an Azure Active Directory account. Use a domain Active Directory account instead.

### Scalability Capabilities

| | Azure Analysis Services | SQL Server Analysis Services | SQL Server in Azure Virtual Machine + Columnstore Indexes | Azure SQL Database + Columnstore Indexes |
| --- | --- | --- | --- | --- |
| Redundant regional servers for high availability  | [Yes](https://docs.microsoft.com/azure/analysis-services/analysis-services-bcdr) | No | Yes | Yes |
| Supports query scale out  | Yes | No | Yes | No |
| Dynamic scalability (scale up)  | Yes | No | Yes | No |

## <a name="wheretogo"></a>Where to go from here
Read next:
[Data Warehousing pipeline pattern](../pipeline-patterns/data-warehousing.md)

See also:

Related pipeline patterns
- Working with transactional data
    - [Online Transaction Processing (OLTP)](../pipeline-patterns/online-transaction-processing.md)
    - [Online Analytical Processing (OLAP)](../pipeline-patterns/online-analytical-processing.md)
    - [Data Warehousing](../pipeline-patterns/data-warehousing.md)

Related technology choices
- Transactional data stores
    - [Online Transaction Processing (OLTP) data stores](../technology-choices/oltp-data-stores.md)
    - [Data Warehouses](../technology-choices/data-warehouses.md)
    - [Data serving storage](../technology-choices/data-serving-storage.md)
    - [Options for Pipeline Orchestration, Control Flow, and Data Movement](../technology-choices/pipeline-orchestration-data-movement.md)
