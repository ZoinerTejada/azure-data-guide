# Options for processing CSV and JSON files

[About]()  
[What are your options for processing CSV and JSON files?](#options)  
[How do you choose?](#howtochoose)  
[Key Selection Criteria](#criteria)  
[Capability Matrix](#matrix)   
[Where to go from here](#wheretogo)  

<a name="about"></a>

## <a name="options"></a> What are your options for processing CSV and JSON files?
In Azure, the following services will help you process CSV and JSON files:
- Azure Data Factory
- Azure Logic Apps
- Azure Functions
- App Service
- Azure Data Lake Analytics
- Azure HDInsight
    - Spark SQL
    - HBase
    - Hive
- SQL Data Warehouse
- Azure Machine Learning Workbench
- SQL SSIS

Whether you are importing your CSV and JSON files into Azure Storage/Azure Data Lake Store, or processing and loading the data into a database such as Azure SQL, SQL DW, or Cosmos DB, [Azure Data Factory](https://docs.microsoft.com/azure/data-factory/copy-activity-overview) provides a great option to automate the process for either one-time or recurring operations. Use the copy activity to copy your on-premises or cloud-based files into a number of [supported data stores](https://docs.microsoft.com/azure/data-factory/copy-activity-overview#supported-data-stores-and-formats).

Once stored, there are a number of options for processing your files. Because many programming languages can easily work with CSV and JSON files from applications that run on a virtual machine or locally, we are going to focus on Azure services you can use, some of which require no programming.

Starting out with a visual design-driven option for working with CSV and JSON files, you could use [Azure Logic Apps](https://docs.microsoft.com/azure/logic-apps/) to create an automated workflow that processes these files, and translates them to another format, such as XML, or sends the data to a connected service or mobile device. You use an [integration account](https://docs.microsoft.com/azure/logic-apps/logic-apps-enterprise-integration-create-integration-account) and link it to your logic app to [work with your flat files](https://docs.microsoft.com/azure/logic-apps/logic-apps-enterprise-integration-flatfile). What you get out of Flat Files decoding is an XML document and you may further convert that document to JSON using the [workflow definition language](https://docs.microsoft.com/azure/logic-apps/logic-apps-workflow-definition-language) json() function. In the opposite direction, you may convert JSON data to XML content using the xml() function of the workflow definition language.

An option that requires coding, but still allows you not have to manage infrastructure due to its serverless nature, is to use [Azure Functions](https://docs.microsoft.com/azure/azure-functions/). Azure Functions is an event driven, compute-on-demand service that helps you implement code triggered by events occurring in virtually any Azure or 3rd party service as well as on-premisis systems. In one scenario, you may have a process that stores your CSV or JSON files in blob storage, then create an Azure Function that is triggered any time a file is added, to do some processing of that file. Another option is to use a webhook trigger on an Azure Function to parse and process JSON data sent from an online service like GitHub or Salesforce. Since Azure Functions can be written in C#, F#, Node.js, or Python, it is very easy to write code that can work CSV and JSON files. There are also [many bindings](https://docs.microsoft.com/azure/azure-functions/functions-reference#bindings) for triggering functions, automatically working with inputs, and outputting processed information.

Process CSV and JSON files through web and API apps with [App Service](https://docs.microsoft.com/azure/app-service/) for a more traditional web-based approach. Create web apps that can accept CSV and JSON files that are uploaded, or stored in Azure Storage or Azure Data Lake Store for processing, using .NET, .NET Core, Java, Ruby, Node.js, PHP, or Python.

When you need a big data solution, use [Azure HDInsight](https://docs.microsoft.com/azure/hdinsight/), a managed Open Source Big Data analytics service for the enterprise. With it, you can create and use optimized Hadoop, Spark, Hive, HBase, Storm, Kafka, and Microsoft R Server clusters to process and analyze your files at scale. Another option in this space is [Azure Data Lake Analytics](https://docs.microsoft.com/azure/data-lake-analytics/), which runs massively parallel data transformation and processing programs using a T-SQL/C# hybrid called U-SQL, R, Python, and .NET over petabytes of data. Its capabilities for working with CSV and JSON files is mostly in line with HDInsight for batch operations. If you are interested in real-time stream processing of your files, such as live log analytics, HDInsight offers options for doing so with Hadoop technologies like Spark, HBase, and Storm.

If you would like to use advanced data preparation tools for efficiently exploring, understanding, and fixing problems in your source CSV or JSON data, consider using [Data Preparation](https://docs.microsoft.com/azure/machine-learning/preview/data-prep-getting-started) as part of the [Azure Machine Learning Workbench](https://docs.microsoft.com/azure/machine-learning/preview/scenario-big-data) experience. You can work with files stored locally, or in Azure Blob Storage. Once you have prepared your data, you can export it to another datastore more suitable for querying, or use it do develop a machine learning model using different compute targets, like Ubuntu DSVM or an Azure HDInsight cluster, for experimentation.

Consider using [SQL Data Warehouse](https://docs.microsoft.com/azure/sql-data-warehouse/) when you need to integrate your relational and non-relational data, such as data stored in CSV and JSON files, in a cloud-based, scale-out database capable of processing massive volumes of data. This is an ideal solution for those more comfortable with using SQL Server Transact-SQL (T-SQL) and related tools. PolyBase is what allows SQL Data Warehouse to access and combine both non-relational and relational data. It allows you to run queries on external data in Hadoop or Azure blob storage. PolyBase uses external tables to access data in Azure Blob storage. By simply using Transact-SQL (T-SQL) statements, you can import and export data back and forth between relational tables in SQL Server and non-relational data stored in Hadoop or Azure Blob Storage. You can also query the external data using a T-SQL query and join it with relational data. However, the most common use of PolyBase is to load data into the data warehouse as part of the ETL process, rather than performing ad-hoc queries against CSV and JSON files.

[SQL Server Integration Services](https://docs.microsoft.com/sql/integration-services/sql-server-integration-services) (SSIS) is a platform for data integration and workflow applications capable of a broad range of data migration tasks. SSIS can be used to extract and transform data from a wide variety of sources such as CSV and JSON files, and then load the data into one or more destinations. Consider using SSIS for these tasks as part of your ETL process when using SQL Server or SQL Data Warehouse as your data store.

## <a name="howtochoose"></a> How do you choose?
Each service brings with it a unique set of capabilities, giving you options in selecting the one that most closely meets your requirements. You need to consider your specific challenges, like scale. Do you need to process one at a time, in large batches, or lots of incoming files streaming in real-time?

## <a name="criteria"></a> Key Selection Criteria

Answer the following questions to help you narrow down your choices, then use the matrices below to select your options for your scenario:

- Do you need big data capabilities for processing your files? Usually this means multi-gigabytes to terabytes of data.
    - If yes, then narrow your options to those that are big data services.
- Does your solution require moving data stored in one location into another?
    - If so, also look at the orchestration options.
- Does your data arrive via REST endpoints or through uploads through a web application?
    - If yes, compare options provided in the Compute category.
- Does your data need to be processed in real-time? In other words, do you need to process streaming data?
    - If so, consider the options that provide stream processing.
- Do you need to be able to re-process large amounts of data?
    - If so, select one of the big data options.

## <a name="matrix"></a> Capability Matrix

Capabilities are separated into the following categories: Big Data, Machine Learning, Compute, and Orchestration. These categories help compare like-services, due to the breadth of options and scenarios for processing CSV and JSON files.

### Big Data Capabilities

When you need to work with very large data sets, or process streaming data in real-time, compare the capabilities of these big data services:

| | Azure Data Lake Analytics | HDInsight |
| --- | --- | --- |
| Is Managed Service | Yes | Yes - but requires manual configuration and scaling |
| Batch Processing | Yes | Yes |
| Stream (Real-time Processing) | No | Yes - using Spark Streaming, Storm, and/or Kafka |
| Interactive Queries | No | Yes - using [Spark](https://azure.microsoft.com/services/hdinsight/apache-spark/) or [HDInsight Interactive Query (Hive LLAP)](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-use-interactive-hive) |
| Programmability | U-SQL (combination of C# and T-SQL) | Python, Scala, Java, SQL (via Spark SQL or HiveQL), C# (when using Storm) |
| Scalability | Can scale individual queries | Scale by adding additional worker nodes |
| Install Additional Software | No | Yes - [manually](https://docs.microsoft.com/azure/hdinsight/hdinsight-apps-install-custom-applications) or through the [Marketplace](https://docs.microsoft.com/azure/hdinsight/hdinsight-apps-install-applications) |
| Cost Platform | Only pay for processing (analytic units) | Pay by the hour for lifetime of the cluster |

### Compute Capabilities

TODO: SHOULD WE RENAME THIS CATEGORY?

Services in this category encompass serverless and web-based solutions for processing your CSV and JSON files. Serverless does not mean there are no servers, just that developers and admins do not need to worry about provisioning or managing servers.

Azure Functions and SQL Data Warehouse are both useful for streaming/real-time processing scenarios. For example, Azure Functions can be used directly by Cosmos DB to create a serverless, globally distributed microservices apps, providing real-time customer experiences based on data and events. The natural choice between CSV and JSON files in this scenario is JSON. SQL Data Warehouse, on the other hand, can be used in an architecture that captures CSV or JSON files and documents in real-time through Kafka on HDInsight or Event Hubs, processed in real-time using Spark or Storm on HDInsight, or with Stream Analytics, then ingested into SQL Data Warehouse through micro-batching offered by Event Grid, which sends processed data using PolyBase.

| | Logic Apps | Azure Functions | App Services | SQL Data Warehouse |
| --- | --- | --- | --- | --- |
| Programmability | None (uses workflow definition language) | C#, F#, Node.js, Python | .NET, .NET Core, Java, Ruby, Node.js, PHP, Python | T-SQL |
| Development Model | Visual Designer | Web application, WebJobs for background tasks | Functions with triggers | Stored procedures, views, dynamic SQL, PolyBase, Massively Parallel Processing (MPP) |
| Serverless | Yes | Yes | No | No |
| Stream (Real-time Processing) | No | Yes | No | Yes |

### Orchestration

When it comes to orchestration, Azure Data Factory (ADF) and SSIS both offer a multitude of data sources and destinations you can use to move and transform your CSV and JSON file data. When your data destination is an Azure service, such as Azure Storage or HDInsight, ADF is the natural choice.

| | Azure Data Factory (ADF) | SQL Server Integration Services (SSIS) |
| --- | --- | --- |
| Managed | Yes | No |
| Cloud-based | Yes | No (local) |
| Prerequisite | Azure Subscription | SQL Server  |
| Management Tools | Azure Portal, PowerShell, CLI, .NET SDK | SSMS, PowerShell |
| Pricing | Pay per usage | Licensing / Pay for features |
| Copy Data | Yes | Yes |
| Custom Transformations (C#) | Yes | Yes |
| Azure ML Scoring | Yes | Yes (with scripting) |
| HDInsight On-Demand | Yes | No |
| Azure Batch | Yes | No |
| Pig and Hive | Yes | No |

## <a name="wheretogo"></a>Where to go from here
Read Next:
Data Warehouse Solution Pattern

See Also:

Related Solution Patterns
- Working with transactional data
    - [Online Transaction Processing (OLTP)](../solution-patterns/online-transaction-processing.md)
    - Online Analytical Processing (OLAP)
    - Data Warehousing

Related Technology Choices
- Transactional data stores
    - [Online Analytical Processing (OLAP) data stores](../technology-choices/olap-data-stores.md)
    - [Data Warehouses](../technology-choices/data-warehouses.md)
