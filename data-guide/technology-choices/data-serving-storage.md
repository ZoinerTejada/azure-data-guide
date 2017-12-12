# Data Serving Storage (aka analytical data store)

[About]()  
[What are your options when choosing data serving storage?](#options)  
[How do you choose?](#howtochoose)  
[Key Selection Criteria](#criteria)  
[Capability Matrix](#matrix)   
[Where to go from here](#wheretogo)  

<a name="about"></a>

In the [Big Data](../common-architectures/big-data.md) common architecture, we reviewed the overall layout and uses of both the lambda and kappa architectures. Both of these pipelines require an analytical data store that serves processed data in a structured format that can be queried using analytical tools. The analytical data stores that support querying of both hot path data and cold path data by client applications and BI tools are collectively referred to as the serving layer, or data serving storage.

The serving layer deals with processed data from both the hot path and cold path. This can be further subdivided into a speed serving layer that stores a subset of incrementally processed hot path data not yet processed by the batch techniques of the cold path, and a batch serving layer that contains the batch-processed output of the cold path. Because of this, the serving layer requires strong support for random reads with low latency. In addition, data serving storage for the speed layer should also support random writes, since any preparation work needed to create to create a batch and batch load data into this store would typically introduce undesired delays. On the other hand, data serving storage for the batch layer does not need to support random writes, but batch writes instead.

There is no single best data management choice for all data storage tasks; different data management solutions are optimized for different tasks. Most real-world cloud apps and big data processes have a variety of data storage requirements and are often served best by a combination of multiple data storage solutions.

## <a name="options"></a> What are your options when choosing data serving storage?
There are several options for data serving storage in Azure, depending on your needs:

- [SQL Data Warehouse](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-overview-what-is)
- [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/)
- [SQL Server in Azure VM](https://docs.microsoft.com/sql/sql-server/sql-server-technical-documentation)
- [HBase/Phoenix on HDInsight](https://docs.microsoft.com/azure/hdinsight/hbase/apache-hbase-overview)
- [Hive LLAP on HDInsight](https://docs.microsoft.com/azure/hdinsight/interactive-query/apache-interactive-query-get-started)
- [Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-overview)
- [Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/)

These options provide various database models that are optimized for different types of tasks:

- [Key/value](https://msdn.microsoft.com/en-us/library/dn313285.aspx#sec7) store a single serialized object for each key value. They're good for storing large volumes of data where you want to get one item for a given key value and you don't have to query based on other properties of the item.
- [Document](https://msdn.microsoft.com/en-us/library/dn313285.aspx#sec8) are key/value databases in which the values are *documents*. "Document" here isn't used in the sense of a Word or Excel document but means a collection of named fields and values, any of which could be a child document. For example, in an order history table an order document might have order number, order date, and customer fields; and the customer field might have name and address fields. The database encodes field data in a format such as XML, YAML, JSON, or BSON; or it can use plain text. One feature that sets document databases apart from key/value databases is the ability to query on non-key fields and define secondary indexes to make querying more efficient. This ability makes a document database more suitable for applications that need to retrieve data based on criteria more complex than the value of the document key. For example, in a sales order history document database you could query on various fields such as product ID, customer ID, customer name, and so forth.
- [Column-family](https://msdn.microsoft.com/en-us/library/dn313285.aspx#sec9) are key/value data stores that enable you to structure data storage into collections of related columns called column families. For example, a census database might have one group of columns for a person's name (first, middle, last), one group for the person's address, and one group for the person's profile information (DOB, gender, etc.). The database can then store each column family in a separate partition while keeping all of the data for one person related to the same key. You can then read all profile information without having to read through all of the name and address information as well.
- [Graph](https://msdn.microsoft.com/en-us/library/dn313285.aspx#sec10) store information as a collection of objects and relationships. The purpose of a graph database is to enable an application to efficiently perform queries that traverse the network of objects and the relationships between them. For example, the objects might be employees in a human resources database, and you might want to facilitate queries such as "find all employees who directly or indirectly work for Scott."

## <a name="howtochoose"></a> How do you choose?
Each data serving solution brings with it a unique set of capabilities, giving you options in selecting the one that most closely meets your requirements.

## <a name="criteria"></a> Key Selection Criteria

The following tables summarize the key differences in capabilities between each. For data serving storage scenarios, choose the appropriate system for your needs by answering these questions:

- Do you need serving storage that can serve as a hot path for your data?
    - If yes, narrow your options to those that are optimized for speed serving layer.
- Do you need massively parallel processing (MPP) support, where your queries are automatically distributed amongst several processes or nodes?
    - If so, select an option that supports query scale out.
- Do you prefer to use a relational data store?
    - If so, narrow your options to those with a relational database model, but also note that it is possible to use a tool like PolyBase to query non-relational data stores if needed.

## <a name="matrix"></a> Capability Matrix

### General Capabilities

| | Azure SQL Database | SQL Server in Azure VM | SQL Data Warehouse | HBase/Phoenix on HDInsight | Hive LLAP on HDInsight | Azure Analysis Services | Cosmos DB |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Is managed service | Yes | | No | Yes | Yes - with manual configuration/scaling | Yes - with manual configuration/scaling | Yes | Yes |
| Primary database model | Relational (columnar format when using columnstore indexes) | Relational (columnar format when using columnstore indexes) | Relational tables with columnar storage | Wide column store | Hive/In-Memory | Tabular/MOLAP semantic models | Document store, Graph DBMS, Key-value store, Wide column store |
| SQL syntax support | Yes | Yes | Yes | Yes (using the [Phoenix](http://phoenix.apache.org/) JDBC driver) | Yes | No | Yes |
| Optimized for speed serving layer | Yes, using memory-optimized tables and hash or nonclustered indexes | Yes, using memory-optimized tables and hash or nonclustered indexes | No | Yes | Yes | No | Yes |
| Regional availability | See [here](https://azure.microsoft.com/regions/#services) | See [here](https://azure.microsoft.com/regions/#services) | See [here](https://azure.microsoft.com/regions/#services) | See [here](https://azure.microsoft.com/regions/#services) | See [here](https://azure.microsoft.com/regions/#services) | See [here](https://azure.microsoft.com/regions/#services) | See [here](https://azure.microsoft.com/regions/#services) |

### Scalability Capabilities

| | Azure SQL Database | SQL Server in Azure VM | SQL Data Warehouse | HBase/Phoenix on HDInsight | Hive LLAP on HDInsight | Azure Analysis Services | Cosmos DB |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Redundant regional servers for high availability  | Yes | Yes | Yes | Yes | No | No | Yes | Yes |
| Supports query scale out  | No | No | Yes | Yes | Yes | Yes | Yes |
| Dynamic scalability (scale up)  | Yes | No | Yes | No | No | Yes | Yes |
| Supports in-memory caching of data | Yes | Yes | Yes | No | Yes | Yes | No |

### Security Capabilities

| | Azure SQL Database | SQL Server in Azure VM | HBase/Phoenix on HDInsight | Hive LLAP on HDInsight | Azure Analysis Services | Cosmos DB |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Authentication  | SQL / Azure Active Directory | SQL / Azure Active Directory | SQL / Azure Active Directory | local / Azure Active Directory * | local / Azure Active Directory * | Azure Active Directory | database users / Azure Active Directory via Access control (IAM) |
| Authorization  | Yes | Yes | Yes | Yes * | Yes * | Yes | [Yes](https://docs.microsoft.com/azure/cosmos-db/secure-access-to-data) (hash-based message authentication code (HMAC))
| Auditing  | Yes | Yes | Yes | Yes * | Yes * | Yes (when integrated with [Azure Monitor Resource Diagnostic Logs](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)) | Yes (through [audit logging/activity logs](https://docs.microsoft.com/azure/cosmos-db/logging))
| Data encryption at rest | Yes ** | Yes ** | Yes ** | Yes * | Yes * | Yes | Yes |
| Row-level security | Yes | Yes | No | Yes * | Yes * | Yes (through object-level security in model) | No |
| Supports firewalls | Yes | Yes | Yes | Yes \*** | Yes \*** | Yes | Yes |
| Dynamic data masking | Yes | Yes | No | Yes * | Yes * | No | No |

\* Requires using a [domain-joined HDInsight cluster](https://docs.microsoft.com/azure/hdinsight/domain-joined/apache-domain-joined-introduction).

\** Requires using Transparent Data Encryption (TDE) to encrypt and decrypt your data at rest.

\*** Supported when [used within an Azure Virtual Network](https://docs.microsoft.com/azure/hdinsight/hdinsight-extend-hadoop-virtual-network) (VNet).


## <a name="wheretogo"></a>Where to go from here
See Also:

Related Pipeline Patterns
- [Handling Time Series Data](../pipeline-patterns/time-series.md)

Related Technology Choices
- [Data Ingest](./data-ingest.md)
- [Real-Time Processing](./real-time-processing.md)