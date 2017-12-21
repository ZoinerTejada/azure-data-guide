# Data Warehouses

[About]()  
[What are your options when choosing a data warehouse?](#options)  
[How do you choose?](#howtochoose)  
[Key selection criteria](#criteria)  
[Capability matrix](#matrix)   
[Where to go from here](#wheretogo)  

<a name="about"></a>

## <a name="options"></a> What are your options when choosing a data warehouse?
There are several options for implementing a data warehouse in Azure, depending on your needs:<!--I would probably have the text below these options first. In fact, I originally had a comment about whether we needed to spell out SMP and MPP for the audience. If the reader isn't familiar with these concepts would they really benefit from going off and reading the material at the links without the context provided by the info below?-->

SMP (small/medium data):

- [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/)
- [SQL Server in a virtual machine](https://docs.microsoft.com/sql/sql-server/sql-server-technical-documentation)

MPP (big data):

- [Azure Data Warehouse](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-overview-what-is)
- [Apache Hive on HDInsight](https://docs.microsoft.com/azure/hdinsight/hadoop/hdinsight-use-hive)
- [Interactive Query (Hive LLAP) on HDInsight](https://docs.microsoft.com/azure/hdinsight/interactive-query/apache-interactive-query-get-started)

The list above is broken into two categories: [SMP](https://en.wikipedia.org/wiki/Symmetric_multiprocessing) (symmetric multiprocessing) and [MPP](https://en.wikipedia.org/wiki/Massively_parallel) (massively parallel). As a general rule, SMP-based warehouses are best suited for small to medium data sets (up to 4-100 TB), while MPP is oftentimes used for big data. The delineation between small/medium and big data has, in part, to do with your organization's definition and supporting infrastructure, as well as the [limitation of the data sizes imposed by the technology choices within](oltp-data-stores.md#scalability-capabilities) your infrastructure. Beyond data sizes, the type of workload pattern you plan to support are likely a greater determining factor. For instance, complex queries may be too slow for an SMP solution, and require an MPP solution instead. MPP-based systems are likely to impose a performance penalty with small data sizes, due to how jobs are distributed and consolidated across nodes. If your data sizes are already exceeding 1 TB and are expected to continually grow, you may want to consider selecting an MPP solution.

As mentioned in the [data warehousing pipeline pattern](../pipeline-patterns/data-warehousing.md#data-warehousing-in-azure) article, the data accessed or stored by your data warehouse could come from a number of data sources, including a [data lake](../common-architectures/big-data.md#datalake), such as [Azure Data Lake Store](https://docs.microsoft.com/azure/data-lake-store/). For a video session that compares the different strengths of MPP services that can use Azure Data Lake, see [Azure Data Lake and Azure Data Warehouse: Applying Modern Practices to Your App](https://azure.microsoft.com/resources/videos/build-2016-azure-data-lake-and-azure-data-warehouse-applying-modern-practices-to-your-app/).

SMP systems are characterized by a single instance of a relational database management system (DBMS) sharing all resources (CPU/Memory/Disk&mdash;that is, shared everything). MPP solutions, on the other hand, require a different skillset, due to variances in querying, modeling, partitioning of data, and other factors unique to parallel processing. One quick way to remember the difference is that you can scale-up an SMP system by adding processors with more CPU cores or faster CPU cores, add more memory, and use a faster I/O subsystem. For an MPP system you can scale-out by adding more compute nodes (which have their own CPU, memory and I/O subsystems). There are physical limitations to scaling up a server, at which point scaling out is more desirable depending on the workload.

When deciding which SMP solution to use, refer to [A closer look at Azure SQL Database (PaaS) and SQL Server on Azure virtual machines (IaaS)](https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas#a-closer-look-at-azure-sql-database-and-sql-server-on-azure-vms). In addition, Azure SQL Data Warehouse can also be used for small and medium datasets, where the workload is compute and memory intensive.

Read more about SQL Data Warehouse patterns and common scenarios:

- [SQL Data Warehouse Patterns and Anti-Patterns](https://blogs.msdn.microsoft.com/sqlcat/2017/09/05/azure-sql-data-warehouse-workload-patterns-and-anti-patterns/)
- [SQL Data Warehouse Loading Patterns and Strategies](https://blogs.msdn.microsoft.com/sqlcat/2017/05/17/azure-sql-data-warehouse-loading-patterns-and-strategies/)
- [Migrating Data to Azure SQL Data Warehouse](https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/)
- [Common ISV Application Patterns Using Azure SQL Data Warehouse](https://blogs.msdn.microsoft.com/sqlcat/2017/09/05/common-isv-application-patterns-using-azure-sql-data-warehouse/)

## <a name="howtochoose"></a> How do you choose?
Each data warehouse solution brings with it a unique set of capabilities, giving you options in selecting the one that most closely meets your requirements.

## <a name="criteria"></a> Key selection criteria

For data warehouse scenarios, choose the appropriate system for your needs by answering these questions:

- Do you want a managed service or do you prefer to manage your own physical or virtual servers?
    - If yes, then narrow your options to those that are managed services.
- Are you working with extremely large data sets or highly complex, long-running queries? This is sometimes referred to as a big data workload.
    - If yes, narrow your options to those under MPP capabilities. Some things to consider when reviewing your options for this question, is whether the data source is structured or unstructured. For unstructured, it may need to be processed in a big data environment like Spark on HDInsight or Azure Databricks, Hive LLAP on HDInsight, or perhaps Azure Data Lake Analytics, all of which can serve as ELT (Extract, Load, Transform) and ETL (Extract, Transform, Load) engines. They can output the processed data into structured data, making it easier to load into SQL Data Warehouse or one of the other options. For structured data, SQL Data Warehouse now has a new performance tier called Optimized for Compute. This is provided for compute-intensive workloads requiring ultra-high performance.
- Do you want to separate your historical data from your current, operational data?
    - If so, select one of the options where [orchestration](pipeline-orchestration-data-movement.md) is required, as these are standalone warehouses optimized for heavy read access and best suited for acting as a separate historical data store.
- Do you need the ability to integrate data from several sources, beyond your OLTP data store?
    - If so, consider options that easily integrate multiple data sources. Along with this consolidation, do you have a multi-tenancy requirement? If so, remove SQL Data Warehouse from your choices, as it is not ideal for this requirement as outlined in the [SQL Data Warehouse Patterns and Anti-Patterns](https://blogs.msdn.microsoft.com/sqlcat/2017/09/05/azure-sql-data-warehouse-workload-patterns-and-anti-patterns/) article.
- Do you prefer to use a relational data store?
    - If so, narrow your options to those with a relational data store, but also note that it is possible to use a tool like PolyBase to query non-relational data stores if needed. If you do decide to use PolyBase, consider running a few performance tests to validate whether it will work fast enough against your unstructured data sets for your workload.
- Do you have real-time reporting requirements?
    - If you require rapid query response times on high volumes of singleton inserts, narrow your options to those that can support real-time reporting.
- Do you need to support a large number of concurrent users and connections?
    - The ability to support a number of concurrent users/connections depends on several factors. When using Azure SQL, refer to the [documented resource limits](https://docs.microsoft.com/azure/sql-database/sql-database-resource-limits) based on your service tier. SQL Server hosted on a virtual machine will rely on the size of the virtual machine and supporting services (type of storage, and so on.) to determine the limit, but [generally supports](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-the-user-connections-server-configuration-option) up to a maximum of 32,767 user connections. SQL Data Warehouse, however, supports a [maximum of 32 concurrent queries](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-develop-concurrency) across 1,024 concurrent connections, though the number of concurrent queries it supports will increase in the future. Consider using complementary services, such as [Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-overview), to overcome such limitations if you do select SQL Data Warehouse.
- What sort of workload do you have?
    - In general, MPP-based warehouse solutions are best suited for analytical, batch-oriented workloads. If your workloads are transactional by nature, with many small read/write operations or multiple row-by-row operations, consider using one of the SMP options. One exception to this guideline is when using stream processing on an HDInsight cluster, such as Spark Streaming, and storing the data within a Hive table.

## <a name="matrix"></a> Capability Matrix

Based on your responses to the questions above, the following tables will help you select the choice that's right for you.

### General capabilities

| | Azure SQL Database | SQL Server in a virtual machine | SQL Data Warehouse | Apache Hive on HDInsight | Hive LLAP on HDInsight |
| --- | --- | --- | --- | --- | --- |
| Is managed service | Yes | No | Yes | Yes&mdash;with manual configuration/scaling | Yes&mdash;with manual configuration/scaling |
| Requires data orchestration (holds copy of data/historical data) | No | No | Yes | Yes | Yes |
| Easily integrate multiple data sources | No | No | Yes | Yes | Yes |
| Supports pausing compute | No | No | Yes | No \*** | No \*** |
| Relational data store | Yes | Yes | Yes | No | No |
| Real-time reporting | Yes | Yes | No | No | Yes |
| Flexible backup restore points | Yes | Yes | No * | Yes ** | Yes ** |
| SMP/MPP | SMP | SMP | MPP | MPP | MPP |

\* With SQL Data Warehouse, you can restore a database to any available restore point within the last seven days. Snapshots start every four to eight hours and are available for seven days. When a snapshot is older than seven days, it expires and its restore point is no longer available.

\** Recommend using an [external Hive metastore](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-provision-linux-clusters#use-hiveoozie-metastore) that can be backed up and restored as needed. Standard backup and restore options that apply to Blob Storage or Data Lake Store can be used for the data, or third party HDInsight backup and restore solutions, such as [Imanis Data](https://azure.microsoft.com/blog/imanis-data-cloud-migration-backup-for-your-big-data-applications-on-azure-hdinsight/) can be used for greater flexibility and ease of use.

\*** HDInsight clusters can be deleted when not needed, then re-created when they are. If you want to do this as a way to reduce cost, you will want to attach an external data store to your cluster so your data is retained when you delete your cluster. You can use Azure Data Factory to automate your cluster's lifecycle by creating an on-demand HDInsight cluster to process your workload, then delete it once the processing is complete.

### Scalability capabilities

| | Azure SQL Database | SQL Server in a virtual machine | SQL Data Warehouse | Apache Hive on HDInsight | Hive LLAP on HDInsight |
| --- | --- | --- | --- | --- | --- |
| Redundant regional servers for high availability  | Yes | Yes | Yes | No | No |
| Supports query scale out (distributed queries)  | No | No | Yes | Yes | Yes |
| Dynamic scalability (scale up)  | Yes | No | Yes * | No | No |
| Supports in-memory caching of data | Yes | Yes | Yes | No | Yes |

\* SQL Data Warehouse allows you to scale up or down compute by [adjusting the number of data warehouse units (DWUs)](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-manage-compute-overview).

### Security capabilities

| | Azure SQL Database | SQL Server in a virtual machine | SQL Data Warehouse | Apache Hive on HDInsight | Hive LLAP on HDInsight |
| --- | --- | --- | --- | --- | --- |
| Authentication  | SQL / Azure Active Directory | SQL / Azure Active Directory | SQL / Azure Active Directory | local / Azure Active Directory * | local / Azure Active Directory * |
| Authorization  | Yes | Yes | Yes | Yes * | Yes * |
| Auditing  | Yes | Yes | Yes | Yes * | Yes * |
| Data encryption at rest | Yes ** | Yes ** | Yes ** | Yes * | Yes * |
| Row-level security | Yes | Yes | No | Yes * | Yes * |
| Supports firewalls | Yes | Yes | Yes | Yes \*** | Yes \*** |
| Dynamic data masking | Yes | Yes | No | Yes * | Yes * |

\* Requires using a [domain-joined HDInsight cluster](https://docs.microsoft.com/azure/hdinsight/domain-joined/apache-domain-joined-introduction).

\** Requires using Transparent Data Encryption (TDE) to encrypt and decrypt your data at rest.

\*** Supported when [used within an Azure Virtual Network](https://docs.microsoft.com/azure/hdinsight/hdinsight-extend-hadoop-virtual-network).

Read more about securing your data warehouse:

* [Securing your SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-security-overview#connection-security)
* [Secure a database in SQL Data Warehouse](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-overview-manage-security)
* [Extend Azure HDInsight using an Azure Virtual Network](https://docs.microsoft.com/azure/hdinsight/hdinsight-extend-hadoop-virtual-network)
* [Enterprise-level Hadoop security with domain-joined HDInsight clusters](https://docs.microsoft.com/azure/hdinsight/domain-joined/apache-domain-joined-introduction)

## <a name="wheretogo"></a>Where to go from here
Read next:
[Online Transaction Processing (OLTP) pipeline pattern](../pipeline-patterns/online-transaction-processing.md)

See also:

Related pipeline patterns
- Working with transactional data
    - [Online Transaction Processing (OLTP)](../pipeline-patterns/online-transaction-processing.md)
    - [Online Analytical Processing (OLAP)](../pipeline-patterns/online-analytical-processing.md)
    - [Data Warehousing](../pipeline-patterns/data-warehousing.md)

Related technology choices
- Transactional data stores
    - [Online Transaction Processing (OLTP) data stores](../technology-choices/oltp-data-stores.md)
    - [Online Analytical Processing (OLAP) data stores](../technology-choices/olap-data-stores.md)
