# Real-Time Processing Technology Choices

[About]()  
[What are your options when choosing a technology for real-time processing?](#options)  
[How do you choose?](#howtochoose)  
[Key selection criteria](#criteria)  
[Capability matrix](#matrix)   
[Where to go from here](#wheretogo)  

<a name="about"></a>
Real-time processing components consume events or messages from either queue or file based storage, with the goal of inspecting, querying, filtering, and aggregating events. Then forwarding the outcome to another message queue, file store, or database. In some cases, they may invoke REST methods that trigger an application function like sending out an alert or updating a real-time visualization. The key requirement of such processing engines is that they are capable of applying their computation to endless streams of data and produce results with minimal latency, in a near real-time fashion.

## <a name="options"></a> What are your options when choosing a technology for real-time processing?
In Azure, all of the following data stores will meet the core requirements supporting real-time processing:
- [Azure Stream Analytics](https://docs.microsoft.com/azure/stream-analytics/)
- [HDInsight with Spark Streaming](https://docs.microsoft.com/en-us/azure/hdinsight/spark/apache-spark-streaming-overview)
- [HDInsight with Storm](https://docs.microsoft.com/en-us/azure/hdinsight/storm/apache-storm-overview)
- [Azure Functions](https://docs.microsoft.com/en-us/azure/azure-functions/functions-overview)
- [Azure App Service WebJobs](https://docs.microsoft.com/en-us/azure/app-service/web-sites-create-web-jobs)

## <a name="howtochoose"></a> How do you choose?
Each service brings with it a unique set of capabilities, giving you the option to select the one that most closely meets your requirements. 

## <a name="criteria"></a> Key Selection Criteria

The following table summarize the key differences in capabilities between each. <!--See note from analysis-visualizations-reporting.md-->For real-time processing scenarios, begin choosing the appropriate service for your needs by answering these questions:
- Do you want a managed service or do you prefer to setup and manage the cluster of virtual machines running the processing?
    - If yes, then narrow your options to those that are managed services.
- Do you want to author stream processing logic declartively (for example, as SQL queries) or imperatively (for example, Java code)?
    - Narrow your options by the programming pardigm (declarative or imperative).
- Do you need built-in support for temporal processing or windowing?
    - If yes, narrow your options to those that support built-in temporal/windowing.
- Does your data arrive in formats besides Avro, JSON, or CSV?
    - If yes, narrow your options to those that support any format using custom code.
- Do you need to scale your processing beyond 1 GB/s?
    - If yes, consider the options that scale with the cluster size. 

## <a name="matrix"></a> Capability matrix

### General capabilities
| | Azure Stream Analytics | HDInsight with Spark Streaming | HDInsight with Storm | Azure Functions | Azure App Service WebJobs |
| --- | --- | --- | --- | --- | --- | 
| Is Managed Service | Yes |Yes | Yes | Yes | Yes |  
| Programmability | Stream analytics query language, JavaScript | Scala, Python, Java | Java, C# | C#, F#, Node.js | C#, Node.js, PHP, Java, Python |
| Programming paradigm | Declarative | Mixture of declarative and imperative | Imperative | Imperative | Imperative |    
| Pricing model | By streaming units | By cluster hour | By cluster hour | Per function execution and resource consumption | Per app service plan hour |  

### Integration capabilities
| | Azure Stream Analytics | HDInsight with Spark Streaming | HDInsight with Storm | Azure Functions | Azure App Service WebJobs |
| --- | --- | --- | --- | --- | --- | 
| Configurable sources | Event Hubs, IoT Hub, Azure Storage Blobs  | Event Hubs, IoT Hub, Kafka, HDFS  | Event Hubs, IoT Hub, Azure Storage Blobs, Azure Data Lake Store  | Service Bus, Azure Storage Queues, Azure Storage Blobs, Event Hubs, WebHooks, HTTP, Azure Cosmos DB, Microsoft Graph | Service Bus, Azure Storage Queues, Azure Storage Blobs, Event Hubs, WebHooks, Azure Cosmos DB, Files |
| Configurable sinks | SQL Database, Azure Storage Blobs, Azure Storage Tables, Event Hubs, Power BI, Service Bus, Azure Cosmos DB, Azure Functions | HDFS |  Event Hubs, Service Bus, Kafka | Service Bus, Azure Storage Queues, Azure Storage Blobs, Event Hubs, WebHooks, HTTP, Azure Cosmos DB, Microsoft Graph | Service Bus, Azure Storage Queues, Azure Storage Blobs, Event Hubs, WebHooks, Azure Cosmos DB, Files | 
| Supports custom sources/sinks | Yes | Yes | Yes | Yes | Yes |  

### Processing capabilities
| | Azure Stream Analytics | HDInsight with Spark Streaming | HDInsight with Storm | Azure Functions | Azure App Service WebJobs |
| --- | --- | --- | --- | --- | --- | 
| Built-in temporal/windowing support | Yes | Yes | Yes | No | No |
| Input data formats | Avro, JSON or CSV, UTF-8 encoded | Any format using custom code | Any format using custom code | Any format using custom code | Any format using custom code |
| Scalability | Up to 1 GB/second | Bounded by cluster size | Bounded by cluster size | Up to 200 function app instances processing in parallel | Bounded by app service plan capacity | 
| Late arrival and out of order event handling support | Yes | Yes | Yes | No | No |


## <a name="wheretogo"></a>Where to go from here
See also: <!--No suggested "Read next" for this one?-->

Related pipeline patterns
- [Handling Time Series Data](../pipeline-patterns/time-series.md)

Related technology choices
- [Data Ingest](./data-ingest.md)



