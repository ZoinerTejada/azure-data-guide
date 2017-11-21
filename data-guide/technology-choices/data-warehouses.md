# Data Warehouses

[About]()  
[What are your options when choosing a data warehouse?](#options)  
[How do you choose?](#howtochoose)  
[Key Selection Criteria](#criteria)  
[Capability Matrix](#matrix)   
[Where to go from here](#wheretogo)  

<a name="about"></a>

## <a name="options"></a> What are your options when choosing a data warehouse?
There are several options for using a data warehouse in Azure, depending on your needs:

SMP (small/medium data):

- [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/)
- [SQL Server in a VM](https://docs.microsoft.com/sql/sql-server/sql-server-technical-documentation)

MPP (big data):

- [Azure Data Warehouse](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-overview-what-is)
- [Apache Hive on HDInsight](https://docs.microsoft.com/azure/hdinsight/hadoop/hdinsight-use-hive)
- [Interactive Query (Hive LLAP) on HDInsight](https://docs.microsoft.com/azure/hdinsight/interactive-query/apache-interactive-query-get-started)

The list above is broken into two categories: [SMP](https://en.wikipedia.org/wiki/Symmetric_multiprocessing) (symmetric multiprocessing) and [MPP](https://en.wikipedia.org/wiki/Massively_parallel) (massively parallel). As a general rule, SMP-based warehouses are best suited for small to medium data sets (up to 4-100 TB), while MPP is oftentimes used for big data. The delineation between small/medium and big data has some to do with your organization's definition and supporting infrastructure, but more so the [limitation of the data sizes imposed by the technology choices within](oltp-data-stores.md#scalability-capabilities). Beyond data sizes, the types of queries you plan to support are also a determining factor. For instance, complex queries, sometimes referred to as "last mile" queries, may be too slow for an SMP solution, and require an MPP solution instead.

## <a name="howtochoose"></a> How do you choose?
Each data warehouse solution brings with it a unique set of capabilities, giving you options in selecting the one that most closely meets your requirements.

## <a name="criteria"></a> Key Selection Criteria

The following tables summarize the key differences in capabilities between each. For OLAP scenarios, choose the appropriate system for your needs by answering these questions:

- Do you want a managed service or do you prefer to manage your own physical or virtual servers?
    - If yes, then narrow your options to those that are managed services.
- Are you working with big data or highly complex, time-intensive queries?
    - If yes, narrow your options to those under MPP Capabilities.
- Do you want to separate your historical data from your current, operational data?
    - If so, select one of the options where [orchestration](pipeline-orchestration-data-movement.md) is required, as these are standalone warehouses optimized for heavy read access and best suited for acting as a separate historical data store.
- Do you need the ability to integrate data from several sources, beyond your OLTP data store?
    - If so, consider options that easily integrate multiple data sources.
- Do you want to be able to pause your data warehouse so you only pay for storage costs when no processing is required?
    - If yes, narrow your options down to those that support pausing compute.
- Do you prefer to use a relational data store?
    - If so, narrow you options to those with a relational data store, but also note that it is possible to use a tool like PolyBase to query non-relational data stores if needed.

## <a name="matrix"></a> Capability Matrix

### General Capabilities

| | Azure SQL Database | SQL Server in a VM | SQL Data Warehouse | Apache Hive on HDInsight | Hive LLAP on HDInsight |
| --- | --- | --- | --- | --- | --- |
| Is managed service | Yes | No | Yes | Yes - with manual configuration/scaling | Yes - with manual configuration/scaling |
| Requires data orchestration (holds copy of data/historical data) | No | No | Yes | Yes | Yes |
| Easily integrate multiple data sources | No | No | Yes | Yes | Yes |
| Supports pausing compute | No | No | Yes | No | No |
| Relational data store | Yes | Yes | Yes | No | No |

### Scalability Capabilities

| | Azure SQL Database | SQL Server in a VM | SQL Data Warehouse | Apache Hive on HDInsight | Hive LLAP on HDInsight |
| --- | --- | --- | --- | --- | --- |
| Redundant regional servers for high availability  | Yes | Yes | Yes | No | No |
| Supports query scale out  | No | No | Yes | Yes | Yes |
| Dynamic scalability (scale up)  | Yes | No | Yes | No | No |

### SMP

| | Azure SQL Database | SQL Server in a VM |
| --- | --- | --- |

### MPP

| | SQL Data Warehouse | Apache Hive on HDInsight | Hive LLAP on HDInsight |
| --- | --- | --- | --- |

## <a name="wheretogo"></a>Where to go from here
Read Next:
[Online Transaction Processing (OLTP) Solution Pattern](../solution-patterns/online-transaction-processing.md)

See Also:

Related Solution Patterns
- Working with transactional data
    - [Online Transaction Processing (OLTP)](../solution-patterns/online-transaction-processing.md)
    - [Online Analytical Processing (OLAP)](../solution-patterns/online-analytical-processing.md)
    - [Data Warehousing](../solution-patterns/data-warehousing.md)

Related Technology Choices
- Transactional data stores
    - [Online Transaction Processing (OLTP) data stores](../technology-choices/oltp-data-stores.md)
    - [Online Analytical Processing (OLAP) data stores](../technology-choices/olap-data-stores.md)
