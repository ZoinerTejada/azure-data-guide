# Batch Processing Technology Choices

[About]()  
[What are your options when choosing a technology for batch processing?](#options)  
[How do you choose?](#howtochoose)  
[Key Selection Criteria](#criteria)  
[Capability Matrix](#matrix)   
[Where to go from here](#wheretogo)  

<a name="about"></a>
Because the data sets are so large, often a big data solution must process data files using long-running batch jobs to filter, aggregate, and otherwise prepare the data for analysis. Usually these jobs involve reading source files from scalable storage (like HDFS, Azure Data Lake Store and Azure Storage), processing them, and writing the output to new files in scalable storage. 

The key requirement of such batch processing engines is that they are capable of applying their computation in a scale out fashion that can handle significant data volumes. Unlike for real-time processing, with batch processing latency (in terms of time until the results are ready) are expected to measure in minutes to hours.   

## <a name="options"></a> What are your options when choosing a technology for batch processing?
In Azure, all of the following data stores will meet the core requirements supporting batch processing:
- [Azure Data Lake Analytics](https://docs.microsoft.com/en-us/azure/data-lake-analytics/)
- [Azure SQL Data Warehouse](https://docs.microsoft.com/en-us/azure/data-lake-analytics/)
- [HDInsight with Spark](https://docs.microsoft.com/en-us/azure/hdinsight/spark/apache-spark-overview)
- [HDInsight with Hive](https://docs.microsoft.com/en-us/azure/hdinsight/hadoop/hdinsight-use-hive)
- [HDInsight with Hive LLAP](https://docs.microsoft.com/en-us/azure/hdinsight/interactive-query/apache-interactive-query-get-started)

## <a name="howtochoose"></a> How do you choose?
Each service brings with it a unique set of capabilities, giving you options in selecting the one that most closely meets your requirements. 

## <a name="criteria"></a> Key Selection Criteria

The following table summarize the key differences in capabilities between each. For real-time processing scenarios, begin choosing the appropriate service for your needs by answering these questions:
- Do you want a managed service or do you prefer to setup and manage the cluster of VM's running the processing?
    - If yes, then narrow your options to those that are managed services.
- Do you want to author batch processing logic declaratively (e.g., as SQL queries) or imperatively (e.g., Python or Java code)?
    - Narrow your options by the programming paradigm (declarative or imperative).
- Do you perform your batch processing in bursts?
    - If yes, consider selecting the options that enable you to pause the cluster or whose pricing model is per batch job.
- Do you need to query relational data stores along with your batch processing, for example to lookup reference data?
    - If yes, consider the options that enable querying of external relational stores.

## <a name="matrix"></a> Capability Matrix

### General Capabilities

| | Azure Data Lake Analytics | SQL Data Warehouse | HDInsight with Spark | HDInsight with Hive | HDInsight with Hive LLAP |
| --- | --- | --- | --- | --- | --- |
| Is managed service | Yes | Yes | Yes - with manual configuration/scaling | Yes - with manual configuration/scaling | Yes - with manual configuration/scaling |
| Supports pausing compute | No | Yes | No | No | No |
| Relational data store | Yes | Yes | No | No | No |
| Programmability | U-SQL | T-SQL | Python, Scala, Java, R | HiveQL | HiveQL |
| Programming Paradigm | Mixture of Declarative and Imperative  | Declarative | Mixture of Declarative and Imperative | Declarative | Declarative | 
| Pricing Model | Per batch job (by resources utilized) | By cluster hour | By cluster hour | By cluster hour | By cluster hour |  

### Integration Capabilities
| | Azure Data Lake Analytics | SQL Data Warehouse | HDInsight with Spark | HDInsight with Hive | HDInsight with Hive LLAP |
| --- | --- | --- | --- | --- | --- |
| Query from Azure Data Lake Store | Yes | Yes | Yes | Yes | Yes |
| Query from Azure Storage | Yes | Yes | Yes | Yes | Yes |
| Query from external relational stores (like Azure SQL Database, SQL Server in VM or Azure SQL Data Warehouse) | Yes | No | Yes | No | No |

### Scalability Capabilities
| | Azure Data Lake Analytics | SQL Data Warehouse | HDInsight with Spark | HDInsight with Hive | HDInsight with Hive LLAP |
| --- | --- | --- | --- | --- | --- |
| Scale-out granularity  | Per job | Per cluster | Per cluster | Per cluster | Per cluster |
| Supports fast scale out (less than 1 minute) | Yes | Yes | No | No | No |
| Supports in-memory caching of data | No | Yes | Yes | No | Yes | 

### Security Capabilities
| | Azure Data Lake Analytics | SQL Data Warehouse | HDInsight with Spark | Apache Hive on HDInsight | Hive LLAP on HDInsight |
| --- | --- | --- | --- | --- | --- |
| Authentication  | Azure Active Directory | SQL / Azure Active Directory | No | local / Azure Active Directory * | local / Azure Active Directory * |
| Authorization  | Yes | Yes| No | Yes * | Yes * |
| Auditing  | Yes | Yes | No | Yes * | Yes * |
| Data encryption at rest | Yes| Yes | Yes | Yes | Yes |
| Row-level security | No | Yes | No | Yes * | Yes * |
| Supports firewalls | Yes | Yes | Yes | Yes \*** | Yes \*** |
| Dynamic data masking | No | No | No | Yes * | Yes * |

\* Requires using a [domain-joined HDInsight cluster](https://docs.microsoft.com/azure/hdinsight/domain-joined/apache-domain-joined-introduction).

\** Requires using Transparent Data Encryption (TDE) to encrypt and decrypt your data at rest.

\*** Supported when [used within an Azure Virtual Network](https://docs.microsoft.com/azure/hdinsight/hdinsight-extend-hadoop-virtual-network) (VNet).

## <a name="wheretogo"></a>Where to go from here
See Also:

Related Solution Patterns
- [Processing CSV and JSON files](../solution-patterns/processing-csv-and-json-files.md)
- [Processing free-form text](../solution-patterns/processing-free-form-text.md)

Related Technology Choices
- [Data Ingest](./data-ingest.md)
- [Real-time Processing](./real-time-processing.md)