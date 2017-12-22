# Data ingest

[About]()  
[What are your options when choosing a data ingest method?](#options)  
[How do you choose?](#howtochoose)  
[Key selection criteria](#criteria)  
[Capability matrix](#matrix)   
[Where to go from here](#wheretogo)  

<a name="about"></a>

## <a name="options"></a> What are your options when choosing a data ingest method?
There are several options for ingesting data into Azure, depending on your needs:

- [File storage](#filestorage)
    - [Azure Storage blobs](https://docs.microsoft.com/azure/storage/blobs/storage-blobs-introduction)
    - [Azure Data Lake Store](https://docs.microsoft.com/azure/data-lake-store/)
- [NoSQL databases](#nosql)
    - [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/)
    - [HBase on HDInsight](http://hbase.apache.org/)
- [Streaming/real-time ingest](#streaming)
    - [Azure Event Hubs](https://docs.microsoft.com/azure/event-hubs/)
    - [Azure IoT Hub](https://docs.microsoft.com/azure/iot-hub/)
    - [Kafka on HDInsight](https://docs.microsoft.com/azure/hdinsight/kafka/apache-kafka-get-started)

### <a name="filestorage"></a> File storage

#### Azure Storage blobs

Azure Storage is a Microsoft-managed cloud service that provides storage that is highly available, secure, durable, scalable, and redundant. Microsoft takes care of maintenance and handles critical problems for you. Azure Storage is the most ubiquitous storage solution Azure provides, due to the number of services and tools that can be used with it.

There are various Azure Storage services you can use to store data. The most flexible service option for storing blobs from a number of data sources is [Blob storage](https://docs.microsoft.com/azure/storage/blobs/storage-blobs-introduction). Blobs are basically files like those that you store on your computer (or tablet, mobile device, and so on). They can be pictures, Microsoft Excel files, HTML files, virtual hard disks (VHDs), big data such as logs, database backups&mdash;pretty much anything. Blobs are stored in containers, which are similar to folders. A container provides a grouping of a set of blobs. All blobs must be in a container. An account can contain an unlimited number of containers. A container can store an unlimited number of blobs.

Azure Storage is an excellent choice for big data and analytics solutions, given its flexibility, high availability, and low cost, compared to other options, such as Azure Data Lake Store. Its option of [three storage tiers](https://docs.microsoft.com/azure/storage/blobs/storage-blob-storage-tiers) allow you to store your data most cost-effectively, depending on how you use it. These include the hot storage tier for frequently accessed data, cool storage tier for less frequently accessed data, and the archive storage tier for rarely accessed data.

After storing files in Blob storage, you can access them from anywhere in the world using URLs, the REST interface, or one of the Azure SDK storage client libraries. Storage client libraries are available for multiple languages, including Node.js, Java, PHP, Ruby, Python, and .NET.

There are three types of blobs&mdash;block blobs, page blobs (used for VHD files), and append blobs.

- **Block blobs** are used to hold ordinary files up to about 4.7 TB. This is the type most commonly used for any form of analytics. 
- **Page blobs** are used to hold random access files up to 8 TB in size. These are used for the VHD files that back virtual machines.
- **Append blobs** are made up of blocks like the block blobs, but are optimized for append operations. These are used for things like logging information to the same blob from multiple virtual machines.

Azure Blob storage can be accessed from Hadoop (available through HDInsight). HDInsight can use a blob container in Azure Storage as the default file system for the cluster. Through a Hadoop distributed file system (HDFS) interface provided by a WASB driver, the full set of components in HDInsight can operate directly on structured or unstructured data stored as blobs. Azure Blob storage can also be accessed via Azure SQL Data Warehouse using its PolyBase feature.

Other options that make Azure Storage a good choice are:

- [Multiple concurrency strategies](https://docs.microsoft.com/azure/storage/common/storage-concurrency?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
- [Flexible disaster recovery and high availability options](https://docs.microsoft.com/azure/storage/common/storage-disaster-recovery-guidance?toc=%2fazure%2fstorage%2fblobs%2ftoc.json), like Geo-redundant storage (GRS) and Read-access geo-redundant storage (RA-GRS)
- [Encryption at rest](https://docs.microsoft.com/azure/storage/common/storage-service-encryption?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) to help protect and safeguard your data
- [Role-Based Access Control (RBAC)](https://docs.microsoft.com/azure/storage/common/storage-security-guide?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#management-plane-security) to control access using Azure Active Directory users and groups

#### Azure Data Lake Store

[Azure Data Lake Store](https://docs.microsoft.com/azure/data-lake-store/) is an enterprise-wide hyper-scale repository for Big Data analytic workloads. Data Lake enables you to capture data of any size, type, and ingestion speed in one single [secure](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-overview#DataLakeStoreSecurity) location for operational and exploratory analytics.

Data Lake Store does not impose any limits on account sizes, file sizes, or the amount of data that can be stored in a data lake. Data is stored durably by making multiple copies and there is no limit on the duration of time that the data can be stored in the Data Lake. In addition to making multiple copies of files to guard against any unexpected failures, Data lake spreads parts of a file over a number of individual storage servers. This improves the read throughput when reading the file in parallel for performing data analytics.

As an alternative to Azure Storage, Data Lake Store can be accessed from Hadoop (available through HDInsight) using the WebHDFS-compatible REST APIs. You may consider using this as an alternative to Azure Storage when your individual or combined file sizes exceed that which is supported by Azure Storage. However, there are [performance tuning guidelines](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-performance-tuning-guidance#optimizing-io-intensive-jobs-on-hadoop-and-spark-workloads-on-hdinsight) you should follow when using Data Lake Store as your primary storage for an HDInsight cluster, with specific guidelines for [Spark](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-performance-tuning-spark), [Hive](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-performance-tuning-hive), [MapReduce](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-performance-tuning-mapreduce), and [Storm](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-performance-tuning-storm). Also, be sure to check Data Lake Store's [regional availability](https://azure.microsoft.com/regions/#services), because it is not available in as many regions as Azure Storage, and it needs to be located in the same region as your HDInsight cluster.

Coupled with Azure Data Lake Analytics, Data Lake Store is specifically designed to enable analytics on the stored data and is tuned for performance for data analytics scenarios. Data Lake Store can also be accessed via Azure SQL Data Warehouse using its PolyBase feature.

### <a name="nosql"></a> NoSQL databases

#### Azure Cosmos DB
 <!--Style guide says it's always Azure Cosmos DB.-->
[Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/) is Microsoft’s globally distributed multi-model database. Azure Cosmos DB was built from the ground up with global distribution and horizontal scale at its core. It offers turnkey global distribution across any number of Azure regions by transparently scaling and replicating your data wherever your users are. Elastically scale throughput and storage worldwide, and pay only for the throughput and storage you need. Azure Cosmos DB guarantees single-digit-millisecond latencies at the 99th percentile anywhere in the world, offers multiple well-defined consistency models to fine-tune performance, and guarantees high availability with multi-homing capabilities.

Azure Cosmos DB is schema-agnostic. It automatically indexes all the data without requiring you to deal with schema and index management. It’s also multi-model, natively supporting document, key-value, graph, and column-family data models. With Azure Cosmos DB, you can access your data using APIs of your choice, as DocumentDB SQL (document), MongoDB (document), Azure Table Storage (key-value), and Gremlin (graph) are all natively supported.

Azure Cosmos DB features:

- [Turnkey global distribution](https://docs.microsoft.com/azure/cosmos-db/distribute-data-globally)
- [Elastic scaling of throughput and storage](https://docs.microsoft.com/azure/cosmos-db/partition-data) worldwide
- Single-digit millisecond latencies at the 99th percentile
- [Five well-defined consistency levels](https://docs.microsoft.com/azure/cosmos-db/consistency-levels)
- Guaranteed high availability

#### HBase on HDInsight

[Apache HBase](http://hbase.apache.org/) is an open-source, NoSQL database that is built on Hadoop and modeled after Google BigTable. HBase provides random access and strong consistency for large amounts of unstructured and semi-structured data in a schemaless database organized by column families.

Data is stored in the rows of a table, and data within a row is grouped by column family. HBase is a schemaless database in the sense that neither the columns nor the type of data stored in them need to be defined before using them. The open-source code scales linearly to handle petabytes of data on thousands of nodes. It can rely on data redundancy, batch processing, and other features that are provided by distributed applications in the Hadoop ecosystem.

The [HDInsight implementation](https://docs.microsoft.com/azure/hdinsight/hbase/apache-hbase-overview) leverages the scale-out architecture of HBase to provide automatic sharding of tables, strong consistency for reads and writes, and automatic failover. Performance is enhanced by in-memory caching for reads and high-throughput streaming for writes. In most cases, you'll want to [create the HBase cluster inside a virtual network](https://docs.microsoft.com/azure/hdinsight/hbase/apache-hbase-provision-vnet) so other HDInsight clusters and applications can directly access the tables.

### <a name="streaming"></a> Streaming/real-time ingest

#### Azure Event Hubs

[Azure Event Hubs](https://docs.microsoft.com/azure/event-hubs/) is a highly scalable data streaming platform and event ingestion service, capable of receiving and processing millions of events per second. Event Hubs can process and store events, data, or telemetry produced by distributed software and devices. Data sent to an event hub can be transformed and stored using any real-time analytics provider or batching/storage adapters. With the ability to provide publish-subscribe capabilities with low latency and at massive scale, Event Hubs serves as the on ramp for Big Data.

#### Azure IoT Hub

[Azure IoT Hub](https://docs.microsoft.com/azure/iot-hub/) is a fully managed service that enables reliable and secure bidirectional communications between millions of IoT devices and a cloud-based back end.

Azure IoT Hub:

* Provides multiple device-to-cloud and cloud-to-device communication options. These options include one-way messaging, file transfer, and request-reply methods.
* Provides built-in declarative message routing to other Azure services.
* Provides a queryable store for device metadata and synchronized state information.
* Enables secure communications and access control using per-device security keys or X.509 certificates.
* Provides extensive monitoring for device connectivity and device identity management events.
* Includes device libraries for the most popular languages and platforms.

IoT Hub is often compared to Event Hubs, and some confusion is common when deciding between the two, due to their similarity. When you are managing an IoT infrastructure, even if the only use case is device-to-cloud telemetry ingress, IoT Hub provides a service that is designed for IoT device connectivity. It continues to expand the value proposition for these scenarios with IoT-specific features. Event Hubs is designed for event ingress at a massive scale, both in the context of inter-datacenter and intra-datacenter scenarios.

It is not uncommon to use a combination of IoT Hub and Event Hubs or [Kafka](https://github.com/Azure/toketi-kafka-connect-iothub) in the same solution. IoT Hub handles the device-to-cloud communication, and Event Hubs or Kafka handles later-stage event ingress into real-time processing engines.

#### Kafka on HDInsight

[Apache Kafka](https://kafka.apache.org/) is an open-source distributed streaming platform that can be used to build real-time data pipelines and streaming applications. Kafka also provides message broker functionality similar to a message queue, where you can publish and subscribe to named data streams. It is horizontally scalable, fault-tolerant, and extremely fast.

[Kafka on HDInsight](https://docs.microsoft.com/azure/hdinsight/kafka/apache-kafka-get-started) provides you with a managed, highly scalable, and highly available service in Azure. Both Kafka and Event Hubs can be used as your stream buffering layer in your real-time data pipeline when ingesting events. Use the [Streaming/real-time ingest capabilities](#streamingreal-time-ingest-capabilities) matrix to compare these options.

Some common use cases for Kafka are:

* **Messaging**: Since it supports the publish-subscribe message pattern, Kafka is often used as a message broker.
* **Activity tracking**: Since Kafka provides in-order logging of records, it can be used to track and re-create activities. For example, user actions on a web site or within an application.
* **Aggregation**: Using stream processing, you can aggregate information from different streams to combine and centralize the information into operational data.
* **Transformation**: Using stream processing, you can combine and enrich data from multiple input topics into one or more output topics.

## <a name="howtochoose"></a> How do you choose?

Each data ingest service brings with it a unique set of capabilities, giving you the option to select the one that most closely meets your requirements.

## <a name="criteria"></a> Key selection criteria

For data ingest scenarios, choose the appropriate system for your needs by answering these questions:

- Do you need managed, high speed, cloud-based storage for any type of text or binary data?
    - If yes, then select one of the file storage options.
- Do you need file storage that is optimized for parallel analytics workloads and high throughput/IOPS?
    - If yes, then narrow your file storage options to those that are tuned to analytics workload performance.
- Do you need to store your unstructured or semi-structured data in a schemaless database that provides high-speed read access and consistency to your data?
    - If so, select one of the NoSQL options. Compare options for indexing, available database models, and regional availability. Depending on the type of data you need to store and how you want to work with it, the selection of primary database models may be the biggest determining factor.
- Do you need to capture streaming data in real time, from a number of sources (like cloud to cloud, on-premises to cloud, or intra-cloud), but only need high throughput ingestion capabilities without any sort of device management?
    - If yes, narrow your streaming/real-time ingest capability options to those that only enable event ingress. This could potentially save you money when cloud-to-device communications are not needed.
- Do you need two-way communication between your IoT devices and your cloud-based streaming platform?
    - If so, narrow your streaming/real-time ingest capability options to those that provide cloud-to-device communication patterns.
- Does your streaming solution require the ability to manage access for individual devices, and have the ability to revoke access to a specific device?
    - If yes, select the service with a security capability that provides per-device identity and revocable access control.
- Can you use the service in your region?
    - Check the [regional availability for each Azure service](https://azure.microsoft.com/regions/#services) to find out. If the service you want to use is not in your region, or nearby, then that could automatically disqualify it from your options. This is especially true in situations when data sovereignty is a high priority.

## <a name="matrix"></a> Capability matrix

Based on your responses to the questions above, the following tables will help you select the choice that's right for you.

### File storage capabilities

|  | Azure Data Lake Store | Azure Blob Storage containers |
| --- | --- | --- |
| Purpose | Optimized storage for big data analytics workloads |General purpose object store for a wide variety of storage scenarios |
| Use cases | Batch, streaming analytics, and machine learning data such as log files, IoT data, click streams, large datasets | Any type of text or binary data, such as application back end, backup data, media storage for streaming, and general purpose data |
| Key concepts | Data Lake Store account contains folders, which in turn contains data stored as files | Storage account has containers, which in turn has data in the form of blobs |
| Structure | Hierarchical file system | Object store with flat namespace |
| API | REST API over HTTPS | REST API over HTTP/HTTPS |
| Server-side API | Proprietary [WebHDFS-compatible REST API](https://msdn.microsoft.com/library/azure/mt693424.aspx) | [Azure Blob Storage REST API](https://msdn.microsoft.com/library/azure/dd135733.aspx) |
| Hadoop file system client | Yes |Yes |
| Data operations&mdash;authentication | Based on [Azure Active Directory Identities](https://docs.microsoft.com/azure/active-directory/active-directory-authentication-scenarios) | Based on shared secrets [Account Access Keys](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account#manage-your-storage-account) and [Shared Access Signature Keys](https://docs.microsoft.com/azure/storage/common/storage-dotnet-shared-access-signature-part-1), and [Role-Based Access Control (RBAC)](https://docs.microsoft.com/azure/security/security-storage-overview) |
| Data operations&mdash;authentication protocol | OAuth 2.0. Calls must contain a valid JWT (JSON web token) issued by Azure Active Directory | Hash-based message authentication code (HMAC). Calls must contain a Base64-encoded SHA-256 hash over a part of the HTTP request. |
| Data operations&mdash;authorization | POSIX access control lists (ACLs). ACLs based on Azure Active Directory identities can be set file and folder level. | For account-level authorization use [Account Access Keys](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account#manage-your-storage-account)<br>For account, container, or blob authorization use [Shared Access Signature Keys](https://docs.microsoft.com/azure/storage/common/storage-dotnet-shared-access-signature-part-1) |
| Data Operations&mdash;Auditing | Available. See [here](data-lake-store-diagnostic-logs) for information. |Available |
| Encryption data at rest | <ul><li>Transparent, server side</li> <ul><li>With service-managed keys</li><li>With customer-managed keys in Azure KeyVault</li></ul></ul> | <ul><li>Transparent, server side</li> <ul><li>With service-managed keys</li><li>With customer-managed keys in Azure KeyVault (coming soon)</li></ul><li>Client-side encryption</li></ul> |
| Management operations (for example, account create) | [Role-based access control](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) (RBAC) provided by Azure for account management | [Role-based access control](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) (RBAC) provided by Azure for account management |
| Developer SDKs | .NET, Java, Python, Node.js | .Net, Java, Python, Node.js, C++, Ruby |
| Analytics workload performance | Optimized performance for parallel analytics workloads, High Throughput and IOPS | Not optimized for analytics workloads |
| Size limits | No limits on account sizes, file sizes or number of files | Specific limits documented [here](https://docs.microsoft.com/azure/azure-subscription-service-limits#storage-limits) |
| Geo-redundancy | Locally-redundant (multiple copies of data in one Azure region) | Locally redundant (LRS), globally redundant (GRS), read-access globally redundant (RA-GRS). See [here](https://docs.microsoft.com/azure/storage/common/storage-redundancy) for more information |
| Service state | Generally available | Generally available |
| Regional availability | See [here](https://azure.microsoft.com/regions/#services) | See [here](https://azure.microsoft.com/regions/#services) |
| Price | See [Pricing](https://azure.microsoft.com/pricing/details/data-lake-store/) | See [Pricing](https://azure.microsoft.com/pricing/details/storage/) |

### NoSQL database capabilities

| | Azure Cosmos DB | HBase on HDInsight |
| --- | --- | --- |
| Primary database model | Document store, graph DBMS, key-value store, wide column store | Wide column store |
| Data types | Yes (JSON data types) | No |
| Secondary indexes | Yes | No |
| SQL language support | Yes | Yes (using the [Phoenix](http://phoenix.apache.org/) JDBC driver) |
| Available APIs |<!--DocumentDB is a deprecated name--> [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/documentdb-introduction), [MongoDB](https://docs.microsoft.com/azure/cosmos-db/mongodb-introduction), [Graph](https://docs.microsoft.com/azure/cosmos-db/graph-introduction) (Gremlin), RESTful HTTP, [Table](https://docs.microsoft.com/azure/cosmos-db/table-introduction), [Cassandra](https://docs.microsoft.com/azure/cosmos-db/cassandra-introduction) | Java, RESTful HTTP, Thrift |
| Consistency | Strong, bounded-staleness, session, consistent prefix, eventual | Strong |
| Native Azure Functions integration | [Yes](https://docs.microsoft.com/azure/cosmos-db/serverless-computing-database) | No |
| Regional availability | See [here](https://azure.microsoft.com/regions/#services) | See [here](https://azure.microsoft.com/regions/#services) |
| Automatic global distribution | [Yes](https://docs.microsoft.com/azure/cosmos-db/distribute-data-globally), while maintaining all 5 consistency models | No [HBase cluster replication can be configured](https://docs.microsoft.com/azure/hdinsight/hbase/apache-hbase-replication) across regions with eventual consistency |
| Pricing model | Elastically scalable request units (RUs) charged per-second as needed, elastically scalable storage | Per-minute pricing for HDInsight cluster (horizontal scaling of nodes), storage |

### Streaming/real-time ingest capabilities

| | IoT Hub | Event Hubs | Kafka on HDInsight |
| --- | --- | --- | --- |
| Communication patterns | Enables [device-to-cloud communications](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-d2c-guidance) (messaging, file uploads, and reported properties) and [cloud-to-device communications](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-c2d-guidance) (direct methods, desired properties, messaging) | Only enables event ingress (usually considered for device-to-cloud scenarios) | Only enables event ingress (usually considered for device-to-cloud scenarios) |
| Device state information | [Device twins](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-device-twins) can store and query device state information | No device state information can be stored | No device state information can be stored |
| Device protocol support |Supports MQTT, MQTT over WebSockets, AMQP, AMQP over WebSockets, and HTTPS. Additionally, IoT Hub works with the [Azure IoT protocol gateway](https://docs.microsoft.com/azure/iot-hub/iot-hub-protocol-gateway), a customizable protocol gateway implementation to support custom protocols. <!--This seems redundant. Could we eliminate everything after implementation?--> |Supports AMQP, AMQP over WebSockets, and HTTPS | [Kafka](https://cwiki.apache.org/confluence/display/KAFKA/A+Guide+To+The+Kafka+Protocol) (proprietary binary protocol over TCP) |
| Security |Provides per-device identity and revocable access control. See the [Security section of the IoT Hub developer guide](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-security). | Provides Event Hubs-wide [shared access policies](https://docs.microsoft.com/azure/event-hubs/event-hubs-authentication-and-security-model-overview), with limited revocation support through [publisher's policies](https://docs.microsoft.com/azure/event-hubs/event-hubs-features#event-publishers). IoT solutions are often required to implement a custom solution to support per-device credentials and anti-spoofing measures. | Use SSL or SASL to authenticate connections to brokers from clients. Optional encryption of data transferred between brokers and clients via SSL. Authorization is pluggable. Integration with external auth services supported. Read [security documentation](https://kafka.apache.org/documentation/#security). |
| Operations monitoring | Enables IoT solutions to subscribe to a rich set of device identity management and connectivity events such as individual device authentication errors, throttling, and bad format exceptions. These events enable you to quickly identify connectivity problems at the individual device level. | Exposes only aggregate metrics | [Use Log Analytics](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-oms-log-analytics-tutorial) (part of OMS) to monitor HDInsight clusters. Kafka has a [cluster-specific management solution](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-oms-log-analytics-management-solutions) for Log Analytics. [Additional tools](https://docs.microsoft.com/azure/hdinsight/hdinsight-key-scenarios-to-monitor) can be used to monitor the cluster. |
| Scale | Is optimized to support millions of simultaneously connected devices | Meters the connections as per [Azure Event Hubs quotas](https://docs.microsoft.com/azure/event-hubs/event-hubs-quotas). On the other hand, Event Hubs enables you to specify the partition for each message sent. | Use [Azure Managed Disks](https://docs.microsoft.com/azure/hdinsight/kafka/apache-kafka-scalability) to increase throughput and scalability. Increase number of cluster nodes to scale horizontally. |
| Device SDKs | Provides [device SDKs](https://github.com/Azure/azure-iot-sdks) for a large variety of platforms and languages, in addition to direct MQTT, AMQP, and HTTPS APIs | Is supported on .NET, Java, and C, in addition to AMQP and HTTPS send interfaces | Java, HTTP REST, [other non-Java clients](https://cwiki.apache.org/confluence/display/KAFKA/Clients) |
| File upload | Enables IoT solutions to upload files from devices to the cloud. Includes a file notification endpoint for workflow integration and an operations monitoring category for debugging support. | Not supported | Not supported |
| Route messages to multiple endpoints | Up to 10 custom endpoints are supported. Rules determine how messages are routed to custom endpoints. For more information, see [Send and receive messages with IoT Hub](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-messaging). | Requires additional code to be written and hosted for message dispatching | Kafka partitions streams across the nodes in the HDInsight cluster. Consumer processes can be associated with individual partitions to provide load balancing when consuming records. |

## <a name="wheretogo"></a>Where to go from here
Read next: [Data Pipeline Common Architecture](../common-architectures/data-pipeline.md)

See also:

Related pipeline patterns
- Working with transactional data
    - [Online Transaction Processing (OLTP)](../pipeline-patterns/online-transaction-processing.md)
    - [Online Analytical Processing (OLAP)](../pipeline-patterns/online-analytical-processing.md)
    - [Data Warehousing](../pipeline-patterns/data-warehousing.md)
- Handling text data
    - [Processing CSV and JSON files](../pipeline-patterns/processing-csv-and-json-files.md)
    - [Processing free form text](../pipeline-patterns/processing-free-form-text.md)

Related technology choices
- [Data Transfer Technology Choices](../technology-choices/data-transfer.md)
- [Pipeline Orchestration and Data Movement Technology Choices](../technology-choices/pipeline-orchestration-data-movement.md)
