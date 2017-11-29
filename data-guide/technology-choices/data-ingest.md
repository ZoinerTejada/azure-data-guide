# Data Ingest

[About]()  
[What are your options when choosing a data ingest method?](#options)  
[How do you choose?](#howtochoose)  
[Key Selection Criteria](#criteria)  
[Capability Matrix](#matrix)   
[Where to go from here](#wheretogo)  

<a name="about"></a>

## <a name="options"></a> What are your options when choosing a data ingest method?
There are several options for ingesting data into Azure, depending on your needs:

- [File Storage](#filestorage)
    - Azure Storage Blob Containers
    - Azure Data Lake Store
- [NoSQL Databases](#nosql)
    - Cosmos DB
    - HBase on HDInsight
- [Streaming/Real-time Ingest](#streaming)
    - Event Hubs
    - IoT Hub
    - Kafka on HDInsight

### <a name="filestorage"></a> File Storage

#### Azure Storage Blob Containers

Microsoft Azure Storage is a Microsoft-managed cloud service that provides storage that is highly available, secure, durable, scalable, and redundant. Microsoft takes care of maintenance and handles critical problems for you.

There are various Azure Storage services you can use to store data. The most flexible service option for storing blobs from a number of data sources is [Blob storage](https://docs.microsoft.com/azure/storage/blobs/storage-blobs-introduction). Blobs are basically files like those that you store on your computer (or tablet, mobile device, and so on). They can be pictures, Microsoft Excel files, HTML files, virtual hard disks (VHDs), big data such as logs, database backups -- pretty much anything. Blobs are stored in containers, which are similar to folders. A container provides a grouping of a set of blobs. All blobs must be in a container. An account can contain an unlimited number of containers. A container can store an unlimited number of blobs.

After storing files in Blob storage, you can access them from anywhere in the world using URLs, the REST interface, or one of the Azure SDK storage client libraries. Storage client libraries are available for multiple languages, including Node.js, Java, PHP, Ruby, Python, and .NET.

There are three types of blobs -- block blobs, page blobs (used for VHD files), and append blobs.

- Block blobs are used to hold ordinary files up to about 4.7 TB.
- Page blobs are used to hold random access files up to 8 TB in size. These are used for the VHD files that back VMs.
- Append blobs are made up of blocks like the block blobs, but are optimized for append operations. These are used for things like logging information to the same blob from multiple VMs.

Azure Blob storage can be accessed from Hadoop (available through HDInsight). HDInsight can use a blob container in Azure Storage as the default file system for the cluster. Through a Hadoop distributed file system (HDFS) interface, the full set of components in HDInsight can operate directly on structured or unstructured data stored as blobs.

#### Azure Data Lake Store

[Azure Data Lake Store](https://docs.microsoft.com/azure/data-lake-store/) (ADLS) is an enterprise-wide hyper-scale repository for big data analytic workloads. Azure Data Lake enables you to capture data of any size, type, and ingestion speed in one single [secure](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-overview#DataLakeStoreSecurity) location for operational and exploratory analytics.

ADLS does not impose any limits on account sizes, file sizes, or the amount of data that can be stored in a data lake. Data is stored durably by making multiple copies and there is no limit on the duration of time for which the data can be stored in the data lake. In addition to making multiple copies of files to guard against any unexpected failures, data lake spreads parts of a file over a number of individual storage servers. This improves the read throughput when reading the file in parallel for performing data analytics.

Azure Data Lake Store can be accessed from Hadoop (available through HDInsight) using the WebHDFS-compatible REST APIs. It is specifically designed to enable analytics on the stored data and is tuned for performance for data analytics scenarios. Out of the box, it includes all the enterprise-grade capabilities—security, manageability, scalability, reliability, and availability—essential for real-world enterprise use cases.

### <a name="nosql"></a> NoSQL Databases

#### Cosmos DB

Blah

#### HBase on HDInsight

Blah

### <a name="streaming"></a> Streaming/Real-time Ingest

#### Event Hubs

Blah

#### IoT Hub

Blah

#### Kafka on HDInsight

Blah

## <a name="howtochoose"></a> How do you choose?
Each data ingest solution brings with it a unique set of capabilities, giving you options in selecting the one that most closely meets your requirements.

## <a name="criteria"></a> Key Selection Criteria

The following tables summarize the key differences in capabilities between each. For data ingest scenarios, choose the appropriate system for your needs by answering these questions:

- Do you need to transfer very large amounts of data, where doing so over an internet connection would take too long or be too expensive?
    - If yes, then narrow your options to those that deal with physical media.
- Do you prefer to script your data transfer tasks with the added benefit of reusability and consistency?
    - If so, select one of the command line options, or orchestration if you wish to transfer on a scheduled basis.
- Do you need to transfer data to/from a relational database?
    - If yes, narrow your options to those that support one or more relational databases, taking note of which options also require a Hadoop cluster, which may or may not fit your needs.

## <a name="matrix"></a> Capability Matrix

### File Storage Capabilities

|  | Azure Data Lake Store | Azure Blob Storage Containers |
| --- | --- | --- |
| Purpose | Optimized storage for big data analytics workloads |General purpose object store for a wide variety of storage scenarios |
| Use Cases | Batch, interactive, streaming analytics and machine learning data such as log files, IoT data, click streams, large datasets | Any type of text or binary data, such as application back end, backup data, media storage for streaming and general purpose data |
| Key Concepts | Data Lake Store account contains folders, which in turn contains data stored as files | Storage account has containers, which in turn has data in the form of blobs |
| Structure | Hierarchical file system | Object store with flat namespace |
| API | REST API over HTTPS | REST API over HTTP/HTTPS |
| Server-side API | [WebHDFS-compatible REST API](https://msdn.microsoft.com/library/azure/mt693424.aspx) | [Azure Blob Storage REST API](https://msdn.microsoft.com/library/azure/dd135733.aspx) |
| Hadoop File System Client | Yes |Yes |
| Data Operations - Authentication | Based on [Azure Active Directory Identities](https://docs.microsoft.com/azure/active-directory/active-directory-authentication-scenarios) | Based on shared secrets - [Account Access Keys](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account#manage-your-storage-account) and [Shared Access Signature Keys](https://docs.microsoft.com/azure/storage/common/storage-dotnet-shared-access-signature-part-1). |
| Data Operations - Authentication Protocol | OAuth 2.0. Calls must contain a valid JWT (JSON Web Token) issued by Azure Active Directory | Hash-based Message Authentication Code (HMAC) . Calls must contain a Base64-encoded SHA-256 hash over a part of the HTTP request. |
| Data Operations - Authorization | POSIX Access Control Lists (ACLs). ACLs based on Azure Active Directory Identities can be set file and folder level. | For account-level authorization – Use [Account Access Keys](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account#manage-your-storage-account)<br>For account, container, or blob authorization -  Use [Shared Access Signature Keys](https://docs.microsoft.com/azure/storage/common/storage-dotnet-shared-access-signature-part-1) |
| Data Operations - Auditing | Available. See [here](data-lake-store-diagnostic-logs) for information. |Available |
| Encryption data at rest | <ul><li>Transparent, Server side</li> <ul><li>With service-managed keys</li><li>With customer-managed keys in Azure KeyVault</li></ul></ul> | <ul><li>Transparent, Server side</li> <ul><li>With service-managed keys</li><li>With customer-managed keys in Azure KeyVault (coming soon)</li></ul><li>Client-side encryption</li></ul> |
| Management operations (e.g. Account Create) | [Role-based access control](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) (RBAC) provided by Azure for account management | [Role-based access control](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) (RBAC) provided by Azure for account management |
| Developer SDKs | .NET, Java, Python, Node.js | .Net, Java, Python, Node.js, C++, Ruby |
| Analytics Workload Performance | Optimized performance for parallel analytics workloads. High Throughput and IOPS. | Not optimized for analytics workloads |
| Size limits | No limits on account sizes, file sizes or number of files | Specific limits documented [here](https://docs.microsoft.com/azure/azure-subscription-service-limits#storage-limits) |
| Geo-redundancy | Locally-redundant (multiple copies of data in one Azure region) | Locally redundant (LRS), globally redundant (GRS), read-access globally redundant (RA-GRS). See [here](https://docs.microsoft.com/azure/storage/common/storage-redundancy) for more information |
| Service state | Generally available | Generally available |
| Regional availability | See [here](https://azure.microsoft.com/regions/#services) | See [here](https://azure.microsoft.com/regions/#services) |
| Price | See [Pricing](https://azure.microsoft.com/pricing/details/data-lake-store/) | See [Pricing](https://azure.microsoft.com/pricing/details/storage/) |

### NoSQL Database Capabilities

| | Cosmos DB | HBase on HDInsight |
| --- | --- | --- |

### Streaming/Real-time Ingest Capabilities

| | Event Hubs | IoT Hub | Kafka on HDInsight |
| --- | --- | --- | --- |

## <a name="wheretogo"></a>Where to go from here
Read Next:

TODO: FIGURE OUT WHICH SOLUTION PATTERNS AND TECHNOLOGY CHOICES RELATE/SHOULD BE READ NEXT

See Also:

Related Solution Patterns
- Working with transactional data

Related Technology Choices
- Transactional data stores
