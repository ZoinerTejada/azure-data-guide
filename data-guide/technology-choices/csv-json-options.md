# Online Transaction Processing (OLTP) data stores

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
- Azure Machine Learning
- SQL SSIS

Whether you are importing your CSV and JSON files into Azure Storage/Azure Data Lake Store, or into a database such as Azure SQL or Cosmos DB, [Azure Data Factory](https://docs.microsoft.com/azure/data-factory/copy-activity-overview) provides a great option to automate the process for either one-time or recurring operations. Use the copy activity to copy your on-premises or cloud-based files into a number of [supported data stores](https://docs.microsoft.com/azure/data-factory/copy-activity-overview#supported-data-stores-and-formats).

Once stored, there are a number of options for processing your files. Because many programming languages can easily work with CSV and JSON files from applications that run on a virtual machine or locally, we are going to focus on Azure services you can use, some of which require no programming.

Starting out with a code-free option for working with CSV and JSON files, you could use [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/) to create an automated workflow that processes these files, and translates them to another format, such as XML, or sends the data to a connected service or mobile device. You use an [integration account](https://docs.microsoft.com/azure/logic-apps/logic-apps-enterprise-integration-create-integration-account) and link it to your logic app to [work with your flat files](https://docs.microsoft.com/azure/logic-apps/logic-apps-enterprise-integration-flatfile). What you get out of Flat Files decoding is an XML document and you may further convert that document to JSON using the [workflow definition language](https://docs.microsoft.com/azure/logic-apps/logic-apps-workflow-definition-language) json() function. In the opposite direction, you may convert JSON data to XML content using the xml() function of the workflow definition language.

An option that requires coding, but still allows you not have to manage infrastructure due to its serverless nature, is to use [Azure Functions](https://azure.microsoft.com/services/functions/). Azure Functions is an event driven, compute-on-demand service that helps you implement code triggered by events occurring in virtually any Azure or 3rd party service as well as on-premisis systems. In one scenario, you may have a process that stores your CSV or JSON files in blob storage, then create an Azure Function that is triggered any time a file is added, to do some processing of that file. Another option is to use a webhook trigger on an Azure Function to parse and process JSON data sent from an online service like GitHub or Salesforce. Since Azure Functions can be written in C#, F#, Node.js, or Python, it is very easy to write code that can work CSV and JSON files. There are also [many bindings](https://docs.microsoft.com/azure/azure-functions/functions-reference#bindings) for triggering functions, automatically working with inputs, and outputting processed information.

Process CSV and JSON files through web and API apps with [App Service](https://azure.microsoft.com/services/app-service/) for a more traditional web-based approach. Create web apps that can accept CSV and JSON files that are uploaded, or stored in Azure Storage or Azure Data Lake Store for processing, using .NET, .NET Core, Java, Ruby, Node.js, PHP, or Python.

When you need a big data solution, use [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/), a managed Open Source Big Data analytics service for the enterprise. With it, you can create and use optimized Hadoop, Spark, Hive, HBase, Storm, Kafka, and Microsoft R Server clusters to process and analyze your files at scale. Another option in this space is [Azure Data Lake Analytics](https://azure.microsoft.com/services/data-lake-analytics/), which runs massively parallel data transformation and processing programs using a T-SQL/C# hybrid called U-SQL, R, Python, and .NET over petabytes of data. Its capabilities for working with CSV and JSON files is mostly in line with HDInsight for batch operations. If you are interested in real-time stream processing of your files, such as live log analytics, HDInsight offers options for doing so with Hadoop technologies like Spark, HBase, and Storm.

## <a name="howtochoose"></a> How do you choose?
Each service brings with it a unique set of capabilities, giving you options in selecting the one that most closely meets your requirements. You need to consider your specific challenges, like scale. Do you need to process one at a time, in large batches, or lots of incoming files streaming in real-time?

## <a name="criteria"></a> Key Selection Criteria

Answer the following questions to help you narrow down your choices, then use the matrices below to select your options for your scenario:



## <a name="matrix"></a> Capability Matrix

### General Capabilities


### Scalability Capabilities


### Analytic Workload Capabilities



### Availability Capabilities



### Security Capabilities


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
