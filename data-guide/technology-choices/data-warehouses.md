# Data Warehouses

[About]()  
[What are your options when choosing a data warehouse?](#options)  
[How do you choose?](#howtochoose)  
[Key selection criteria](#criteria)  
[Capability matrix](#matrix)   
[Where to go from here](#wheretogo)  

<a name="about"></a>

## <a name="options"></a> What are your options when choosing a data warehouse?
There are several options for using a data warehouse in Azure, depending on your needs:<!--I would probably have the text below these options first. In fact, I originally had a comment about whether we needed to spell out SMP and MPP for the audience. If the reader isn't familiar with these concepts would they really benefit from going off and reading the material at the links without the context provided by the info below?-->

SMP (small/medium data):

- [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/)
- [SQL Server in a virtual machine](https://docs.microsoft.com/sql/sql-server/sql-server-technical-documentation)

MPP (big data):

- [Azure Data Warehouse](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-overview-what-is)
- [Apache Hive on HDInsight](https://docs.microsoft.com/azure/hdinsight/hadoop/hdinsight-use-hive)
- [Interactive Query (Hive LLAP) on HDInsight](https://docs.microsoft.com/azure/hdinsight/interactive-query/apache-interactive-query-get-started)

The list above is broken into two categories: [SMP](https://en.wikipedia.org/wiki/Symmetric_multiprocessing) (symmetric multiprocessing) and [MPP](https://en.wikipedia.org/wiki/Massively_parallel) (massively parallel). As a general rule, SMP-based warehouses are best suited for small to medium data sets (up to 4-100 TB), while MPP is oftentimes used for big data. The delineation between small/medium and big data has, in part, to do with your organization's definition and supporting infrastructure, but more so the [limitation of the data sizes imposed by the technology choices within](oltp-data-stores.md#scalability-capabilities). <!--Within what? the org or something else. I read this sentence multiple times and couldn't decide. Would "...imposed by your technology choices..." be better here?-->Beyond data sizes, the types of queries you plan to support are also a determining factor. For instance, complex queries <!--"Last mile" is slang, and not in common use on MSDN so I doubt most people use it. I recommend juse deleting this clause.-->may be too slow for an SMP solution, and require an MPP solution instead. MPP-based systems are likely to impose a performance penalty with small data sizes, due to how jobs are distributed and consolidated across nodes. If your data sizes are already exceeding 1 TB and are expected to continually grow, you may want to consider selecting an MPP solution.

SMP systems are characterized by a single instance of a relational database management system (DBMS) sharing all resources (CPU/Memory/Disk&mdash;that is, shared everything). MPP solutions, on the other hand, require a different skillset. This is because within the MPP universe, queries are different, modeling is different, data structures are different, even partitioning of data is different from the comparable structures in an SMP environment.

When deciding which SMP solution to use, refer to [A closer look at Azure SQL Database and SQL Server on Azure virtual machines](https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas#a-closer-look-at-azure-sql-database-and-sql-server-on-azure-vms).<!--Typically I prefer to have the title of the linked doc, rather than "here" or "this "guide" because it allows the reader to decide if they want to go read the topic now or later. It also makes it easier to scan and fine that reference later. I wasn't sure if you want to refer them to the whole linked article or just the section, so you may need to change this depending on that.-->

## <a name="howtochoose"></a> How do you choose?
Each data warehouse solution brings with it a unique set of capabilities, giving you options in selecting the one that most closely meets your requirements.

## <a name="criteria"></a> Key selection criteria

The following tables summarize the key differences in capabilities between each. <!--You might want to move this after the list. It may make more sense to introduce the questions, and then introduce the table with something like: "Based on your responses to the questions, the following table will help you select the choice that's right for you." or something along those lines. Also, BTW, this is one of the best decision making processes I've seen. Normally you get a table that tries to answer all the questions, but doesn't. Breaking it out this way is much easier to follow. -->For OLAP scenarios, choose the appropriate system for your needs by answering these questions:

- Do you want a managed service or do you prefer to manage your own physical or virtual servers?
    - If yes, then narrow your options to those that are managed services.
- Are you working with big data or highly complex, time-intensive queries?
    - If yes, narrow your options to those under MPP capabilities.
- Do you want to separate your historical data from your current, operational data?
    - If so, select one of the options where [orchestration](pipeline-orchestration-data-movement.md) is required, as these are standalone warehouses optimized for heavy read access and best suited for acting as a separate historical data store.
- Do you need the ability to integrate data from several sources, beyond your OLTP data store?
    - If so, consider options that easily integrate multiple data sources.
- Do you want to be able to pause your data warehouse so you only pay for storage costs when no processing is required?
    - If yes, narrow your options down to those that support pausing compute.
- Do you prefer to use a relational data store?
    - If so, narrow your options to those with a relational data store, but also note that it is possible to use a tool like PolyBase to query non-relational data stores if needed.
- Do you have real-time reporting requirements?
    - If you require rapid query response times on high volumes of singleton inserts, narrow your options to those that can support real-time reporting.
- Do you need to support a large number of concurrent users and connections?
    - The ability to support a number of concurrent users/connections depends on several factors. When using Azure SQL, refer to the [documented resource limits](https://docs.microsoft.com/azure/sql-database/sql-database-resource-limits) based on your service tier. SQL Server hosted on a virtual machine will rely on the size of the virtual machine and supporting services (type of storage, and so on.) to determine the limit, but [generally supports](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-the-user-connections-server-configuration-option) up to a maximum of 32,767 user connections. SQL Data Warehouse, however, supports a [maximum of 32 concurrent queries](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-develop-concurrency) across 1,024 concurrent connections. Consider using complementary services, such as [Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-overview), to overcome such limitations if you do select SQL Data Warehouse.
- What sort of workload do you have?
    - In general, MPP-based warehouse solutions are best suited for analytical, batch-oriented workloads. If your workloads are transactional by nature, with many small read/write operations or multiple row-by-row operations, consider using one of the SMP options. One exception to this guideline is when using stream processing on an HDInsight cluster, such as Spark Streaming, and storing the data within a Hive table.

## <a name="matrix"></a> Capability Matrix

### General capabilities

| | Azure SQL Database | SQL Server in a virtual machine | SQL Data Warehouse | Apache Hive on HDInsight | Hive LLAP on HDInsight |
| --- | --- | --- | --- | --- | --- |
| Is managed service | Yes | No | Yes | Yes&mdash;with manual configuration/scaling | Yes&mdash;with manual configuration/scaling |
| Requires data orchestration (holds copy of data/historical data) | No | No | Yes | Yes | Yes |
| Easily integrate multiple data sources | No | No | Yes | Yes | Yes |
| Supports pausing compute | No | No | Yes | No | No |
| Relational data store | Yes | Yes | Yes | No | No |
| Real-time reporting | Yes | Yes | No | No | Yes |
| Flexible backup restore points | Yes | Yes | No * | Yes ** | Yes ** |
| SMP/MPP | SMP | SMP | MPP | MPP | MPP |

\* With SQL Data Warehouse, you can restore a database to any available restore point within the last seven days. Snapshots start every four to eight hours and are available for seven days. When a snapshot is older than seven days, it expires and its restore point is no longer available.

\** Recommend using an [external Hive metastore](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-provision-linux-clusters#use-hiveoozie-metastore) that can be backed up and restored as needed. Standard backup and restore options that apply to Blob Storage or Data Lake Store can be used for the data, or third party HDInsight backup and restore solutions, such as [Imanis Data](https://azure.microsoft.com/blog/imanis-data-cloud-migration-backup-for-your-big-data-applications-on-azure-hdinsight/) can be used for greater flexibility and ease of use.

### Scalability capabilities

| | Azure SQL Database | SQL Server in a virtual machine | SQL Data Warehouse | Apache Hive on HDInsight | Hive LLAP on HDInsight |
| --- | --- | --- | --- | --- | --- |
| Redundant regional servers for high availability  | Yes | Yes | Yes | No | No |
| Supports query scale out  | No | No | Yes | Yes | Yes |
| Dynamic scalability (scale up)  | Yes | No | Yes | No | No |

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
[Online Transaction Processing (OLTP) Solution Pattern](../pipeline-patterns/online-transaction-processing.md)

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
