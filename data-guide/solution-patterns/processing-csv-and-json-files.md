# Processing CSV and JSON files

[About]()  
[When to use this data architecture](#whentouse)  
[Benefits](#benefits)  
[Challenges](#challenges)  
[Processing CSV and JSON files in Azure](#inazure)   
[Where to go from here](#wheretogo)  

<a name="about"></a>
CSV (comma-separated values) files are commonly used to exchange tabular data between systems, in plain text. They typically contain a header row that provides column names for the data, but are otherwise considered unstructured. This is due to the fact that CSVs cannot naturally represent hierarchical or relational data. Data relationships are typically handled with multiple CSV files, where foreign keys are stored in columns of one or more files, but the relationships between those files are not expressed by the format itself. Despite having the moniker "CSV", the term can also be used to denote plain text files that use other delimiters such as tabs or spaces. Though these limitations exist, CSV files are a popular choice for data exchange due to wide ranging support in business, consumer, and scientific applications. For example, database and spreadsheet programs can import and export CSV files, offering options to specify the delimiter and quotation character used within the file. Similarly, most batch and stream data processing engines, such as Spark and Hadoop, natively support serializing and deserializing CSV-formatted files and offer ways to apply a schema on read. This makes it easier to work with the data, by offering options to query against it and store the information in a more performant data format for faster processing.

Data stored in JSON (JavaScript Object Notation) files is represented as key-value pairs in a semi-structured format. JSON is often compared to XML, as both are capable of storing data in hierarchical format, with child data represented inline with its parent. Both are self-describing and human readable, but JSON documents tend to be much leaner, leading to their popular use in online data exchange, especially with the advent of REST-based web services. Since a lot of data coming across the wire is already in JSON format, most web-based programming languages support working with JSON natively, or through the use of external libraries to serialize and deserialized the data stored within. This universal support for JSON has led to its use in logical formats through data structure representation, exchange formats for hot data, and data storage for cold data. This last bit about storage for cold data can mean a couple of things. First, batch and stream data processing engines tend to natively support JSON serlialize/deserialization, similar to CSV-formatted files. Though the data contained within JSON documents may ultimately be stored in a more performance-optimized formats, such as  Parquet or Avro, it serves as the raw data for "source of truth", which is critical for re-processing the data as needed. Secondly, JSON is a commonly used file format for NoSQL databases, such as MongoDB, Couchbase, and Cosmos DB.

## <a name="whentouse"></a>When to use this architecture
The most common use of CSV and JSON files is for exchanging or ingesting data into your environment. CSVs are more commonly used for exporting and importing data that can be used to store the data in a variety of databases, or processing it for analytics and machine learning. JSON-formatted files have the same benefits, but are more prevalent in hot data exchange solutions, where JSON documents are sent across the wire by web and mobile devices performing online transactions, by IoT (internet of things) devices for one-way or bidirectional communication, communicating with SaaS and PaaS services or serverless architectures, as well as between nodes within a microservices architecture. JSON is also commonly used in configuration files and for describing architectural components in a DevOps pipeline, such as [Azure Resource Manager (ARM) templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates).

## <a name="benefits"></a>Benefits
CSV and JSON file formats both have the benefit of making it easy to exchange data between dissimilar systems or devices. Their unstructured, or semi-structured formats, allow flexibility in transferring almost any type of data, and universal support for these formats make them simple to work with. Both can be used as the raw "source of truth" in cases where the data is stored in binary formats that are more performant for querying and accessible for business intelligence and analysis applications and services. This allows for re-processing at any point and working with the data in a different way.

JSON-formatted files have these additional benefits:

* Maintains hierarchical structures, making it easier to hold related data in a single document and represent complex relationships.
* Most programming languages provide native support for deserializing JSON into objects, or provide lightweight libraries to do so.
* Supports lists of objects, helping avoid messy translations of lists into a relational data model.

## <a name="challenges"></a>Challenges
There are some challenges to consider when working with these formats:

* Absent of any restraints on the data model, CSV and JSON files are prone to "garbage in, garbage out". For instance, there's no notion of a date/time object in either file, so the file format does not prevent you from inserting "ABC123" in a date field, for example.
* Striclty using CSV and JSON files as your cold storage solution does not scale well when working with big data. In most cases, they are not splittable into partitions for parallel processing, and cannot be compressed as well as binary formats. This often leads to processing and storing this data into read-optimized formats such as Parquet and ORC (Optimized Row Columnar), which also provide indexes and inline statistics about the data contained.

## <a name="inazure"></a>Processing CSV and JSON files in Azure
Azure provides several solutions for working with CSV and JSON files, depending on your needs.

The primary landing place for these files is either Azure Storage or Azure Data Lake Store. Most Azure services that work with these and other text-based files integrate with either object storage service. In some situations, however, you may opt to directly import the data into Azure SQL or some other data store. When speaking about SQL Server specifically, its native support for storing and working with JSON documents makes it easy to [import and process those types of files](https://docs.microsoft.com/sql/relational-databases/json/import-json-documents-into-sql-server). You can use a utility like SQL Bulk Import to easily [import CSV files](https://docs.microsoft.com/sql/relational-databases/json/import-json-documents-into-sql-server).

Whether you are importing your CSV and JSON files into Azure Storage/Azure Data Lake Store, or into a database such as Azure SQL or Cosmos DB, [Azure Data Factory](https://docs.microsoft.com/azure/data-factory/copy-activity-overview) provides a great option to automate the process for either one-time or recurring operations. Use the copy activity to copy your on-premises or cloud-based files into a number of [supported data stores](https://docs.microsoft.com/azure/data-factory/copy-activity-overview#supported-data-stores-and-formats).

Once stored, there are a number of options for processing your files. Because many programming languages can easily work with CSV and JSON files from applications that run on a virtual machine or locally, we are going to focus on Azure services you can use, some of which require no programming.

Starting out with a code-free option for working with CSV and JSON files, you could use [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/) to create an automated workflow that processes these files, and translates them to another format, such as XML, or sends the data to a connected service or mobile device. You use an [integration account](https://docs.microsoft.com/azure/logic-apps/logic-apps-enterprise-integration-create-integration-account) and link it to your logic app to [work with your flat files](https://docs.microsoft.com/azure/logic-apps/logic-apps-enterprise-integration-flatfile). What you get out of Flat Files decoding is an XML document and you may further convert that document to JSON using the [workflow definition language](https://docs.microsoft.com/azure/logic-apps/logic-apps-workflow-definition-language) json() function. In the opposite direction, you may convert JSON data to XML content using the xml() function of the workflow definition language.

An option that requires coding, but still allows you not have to manage infrastructure due to its serverless nature, is to use [Azure Functions](https://azure.microsoft.com/services/functions/). Azure Functions is an event driven, compute-on-demand service that helps you implement code triggered by events occurring in virtually any Azure or 3rd party service as well as on-premisis systems. In one scenario, you may have a process that stores your CSV or JSON files in blob storage, then create an Azure Function that is triggered any time a file is added, to do some processing of that file. Another option is to use a webhook trigger on an Azure Function to parse and process JSON data sent from an online service like GitHub or Salesforce. Since Azure Functions can be written in C#, F#, Node.js, or Python, it is very easy to write code that can work CSV and JSON files. There are also [many bindings](https://docs.microsoft.com/azure/azure-functions/functions-reference#bindings) for triggering functions, automatically working with inputs, and outputting processed information.

Process CSV and JSON files through web and API apps with [App Service](https://azure.microsoft.com/services/app-service/) for a more traditional web-based approach. Create web apps that can accept CSV and JSON files that are uploaded, or stored in Azure Storage or Azure Data Lake Store for processing, using .NET, .NET Core, Java, Ruby, Node.js, PHP, or Python.

When you need a big data solution, use [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/), a managed Open Source Big Data analytics service for the enterprise. With it, you can create and use optimized Hadoop, Spark, Hive, HBase, Storm, Kafka, and Microsoft R Server clusters to process and analyze your files at scale. Another option in this space is [Azure Data Lake Analytics](https://azure.microsoft.com/services/data-lake-analytics/), which runs massively parallel data transformation and processing programs using a T-SQL/C# hybrid called U-SQL, R, Python, and .NET over petabytes of data. Its capabilities for working with CSV and JSON files is mostly in line with HDInsight for batch operations. If you are interested in real-time stream processing of your files, such as live log analytics, HDInsight offers options for doing so with Hadoop technologies like Spark, HBase, and Storm.

## <a name="wheretogo"></a>Where to go from here
Read Next:
[Data Serving Storage (aka analytical data store) technology choices](../technology-choices/data-serving-storage.md)

See Also:

Related Solution Patterns
- Handling Unstructured Data
    - [Processing Free-form Text](./processing-free-form-text.md)
