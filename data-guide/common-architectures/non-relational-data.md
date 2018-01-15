# Non-Relational Data & No-SQL 

**In this article**

[About]()  
[Common data architectures](#common)   
[Document data](#documentdata)  
[Columnar data](#columnardata)  
[Key/value data](#keyvaluedata)  
[Graph data](#graphdata)  
[Time series data](#timeseriesdata)  
[Object data](#objectdata)  
[External index data](#externalindexdata)  
[Where to go from here](#wheretogo)  

<a name="about"></a>
Non-relational data is not represented in the tabular schema of rows and columns used by many traditional databases, but is instead represented in a storage model that better suits the specific requirements of the application in which the data is used. For example, the data may stored as simple key/value pairs, as JSON documents, or as a graph consisting of edges and vertices. These data stores break from the tradition of representing the data in a relational model and tend to more specific in the type of data they support, and in the ways in which the data can be queried. For example, time series data stores are optimized for supporting queries over time based sequences of data, and graph data stores are optimized for exploring weighted relationships between entities. Neither format would generalize well to the task of managing transactional data. 

No-SQL refers to data stores that do not use SQL for performing their querying, and instead use other programming languages and constructs to query the data. In practice, when the term No-SQL is used, what is really meant is non-relational. This is because overtime, many non-relational data stores have added in SQL compatible query support. So while they have remained non-relational, they are no longer strictly No-SQL.  <!--The MS style to to avoide semicolons because they can make it harder for ESL readers to parse the sentence. They suggest breaking into two.-->

## <a name="common"></a> Common data architectures
There are various non-relational data stores that take their own unique approach to data storage, data representation, data processing, and querying&mdash;and by extension have their own data architecture. The following introduces each.

### <a name="documentdata"></a> Document data stores
A document data store manages a set of named string fields and object data values in an entity referred to as a document. The term document refers to the fact that these data stores typically store their data in the form of JSON documents. Each field value could be a simple scalar item or a compound element, such as a list or a parent-child collection. The data in the fields of a document can be encoded in a variety of ways, including XML, YAML, JSON, BSON, or even stored as plain text. The fields within documents are exposed to the storage management system, enabling an application to query and filter data by using the values in these fields.  

Typically, a document contains the entire data for an entity. What items constitute an entity are application specific. For example, an entity could contain the details of a customer, an order, or a combination of both. A single document might contain information that would be spread across several relational tables in a relational database management system (RDBMS). A document store does not require that all documents have the same structure. This free-form approach provides a great deal of flexibility. For example, applications can store different data in documents in response to a change in business requirements.  

![Example document data store](./images/document.png)  

The application can retrieve documents by using the document key. This is a unique identifier for the document, which is often hashed, to help distribute data evenly. Some document databases create the document key automatically. Others enable you to specify an attribute of the document to use as the key. The application can also query documents based on the value of one or more fields. Some document databases support indexing to facilitate fast lookup of documents based on one or more indexed fields.  

Many document databases support in-place updates, enabling an application to modify the values of specific fields in a document without rewriting the entire document. Read and write operations over multiple fields in a single document are usually atomic.

Relevant Azure service:  
- [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)

### <a name="columnardata"></a> Columnar data stores
A columnar or column-family data store organizes data into columns and rows. In its simplest form, a column-family data store can appear very similar to a relational database, at least conceptually. The real power of a column-family database lies in its denormalized approach to structuring sparse data, which stems from the column- oriented approach to the storage of data taken.  

You can think of a column-family data store as holding tabular data with rows and columns, but the columns are divided into groups known as column families. Each column family holds a set of columns that are logically related together and are typically retrieved or manipulated as a unit. Other data that is accessed separately can be stored in separate column families. Within a column family, new columns can be added dynamically, and rows can be sparse (that is, a row doesn't need to have a value for every column). 

On disk, all of the columns within a column family are stored together in the same file, with a certain quantity of rows (normally dictated by a maximum file size) for the column family present in each file, such that all rows for a column family are spread across multiple files. This approach creates a performance benefit for dealing with big data sets by reducing the amount of data that needs to be read from disk when there are lots of rows, but only a few columns tend to be queried together at a time. This approach also means the related data that is typically needed in the same query, is read during the same read from disk.    

The following diagram shows an example with two column families, Identity and Contact Info. The data for a single entity has the same row key in each column family. This structure, where the rows for any given object in a column family can vary dynamically, is an important benefit of the column-family approach, making this form of data store highly suited for storing data with varying schemas.

![Example of column-family data](./images/column-family.png)

Unlike a key/value store or a document database, most column-family databases physically store data in key order, rather than by computing a hash. The row key is considered the primary index and enables key-based access via a specific key or a range of keys. Some implementations allow you to create secondary indexes over specific columns in a column family. Secondary indexes let you retrieve data by columns value, rather than row key.

Read and write operations for a row are usually atomic within a single column family, although some implementations provide atomicity across the entire row, spanning multiple column families.

Relevant Azure service:  
- [HBase in HDInsight](https://docs.microsoft.com/azure/hdinsight/hdinsight-hbase-overview)

### <a name="keyvaluedata"></a> Key/value data stores
A key/value store is essentially a large hash table. You associate each data value with a unique key, and the key/value store uses this key to store the data by using an appropriate hashing function. The hashing function is selected to provide an even distribution of hashed keys across the data storage.

Most key/value stores only support simple query, insert, and delete operations. To modify a value (either partially or completely), an application must overwrite the existing data for the entire value. In most implementations, reading or writing a single value is an atomic operation. If the value is large, writing may take some time.

An application can store arbitrary data as a set of values, although some key/value stores impose limits on the maximum size of values. The stored values are opaque to the storage system software. Any schema information must be provided and interpreted by the application. Essentially, values are blobs and the key/value store simply retrieves or stores the value by key.

![Example of data in a key/value store](./images/key-value.png)

Key/value stores are highly optimized for applications performing simple lookups using the value of the key, or by a range of keys, but are less suitable for systems that need to query data across different tables of keys/values, such as joining data across multiple tables. 

Key/value stores are also not optimized for scenarios where querying or filtering by non-key values is important, rather than performing lookups based only on keys. For example, with a relational database, you can find a record by using a WHERE clause to filter the non-key columns, but key/values stores usually do not have this type of lookup capability for values or if they do it requires a slow scan of all values.

A single key/value store can be extremely scalable, as the data store can easily distribute data across multiple nodes on separate machines.

Relevant Azure services:  
- [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)  
- [Azure Redis Cache](https://azure.microsoft.com/services/cache/)  
- [Azure Table Storage](https://azure.microsoft.com/services/storage/tables/)

### <a name="graphdata"></a> Graph data stores
A graph data store manages two types of information, nodes and edges. Nodes represent entities, and edges specify the relationships between these entities. Both nodes and edges can have properties that provide information about that node or edge, similar to columns in a table. Edges can also have a direction indicating the nature of the relationship.  

The purpose of a graph data store is to allow an application to efficiently perform queries that traverse the network of nodes and edges, and to analyze the relationships between entities. The follow diagram shows an organization's personnel data structured as a graph. The entities are employees and departments, and the edges indicate reporting relationships and the department in which employees work. In this graph, the arrows on the edges show the direction of the relationships.

![Example of data in a graph data store](./images/graph.png)

This structure makes it straightforward to perform queries such as "Find all employees who report directly or indirectly to Sarah" or "Who works in the same department as John?" For large graphs with lots of entities and relationships, you can perform very complex analyses very quickly. Many graph databases provide a query language that you can use to traverse a network of relationships efficiently.  

Relevant Azure service:  
- [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)  

### <a name="timeseriesdata"></a> Time series data stores
Time series <<!--Not sure why column-family is typically hyphenated when it's a compound modifier and time series is not, but a quick search shows this is the case so I'm leaving it as is.--> data is a set of values organized by time, and a time series data store is optimized for this type of data. Time series data stores must support a very high number of writes, as they typically collect large amounts of data in real time from a large number of sources. Time series data stores are optimized for storing telemetry data. Scenarios include IoT sensors or application/system counters.   

![Example of time series data](./images/time-series.png)

Updates are rare, and deletes are often done as bulk operations. Although the records written to a time series database are generally small, there are often a large number of records, and total data size can grow rapidly. Time series data stores also handle out of order and late-arriving data, automatic indexing of data points, and optimized querying for queries described in terms of windows of time. This last feature enables queries to run across millions of data points and multiple data streams quickly in order to support drill across and drill down behavior in time series visualizations, which is one common way time series data is consumed. 

Relevant Azure service:  
- [Azure Time Series Insights](https://azure.microsoft.com/services/time-series-insights/)  
- [OpenTSDB with HBase on HDInsight](https://docs.microsoft.com/azure/hdinsight/hdinsight-hbase-overview)

### <a name="objectdata"></a> Object data stores
Object data stores are optimized for storing and retrieving large binary objects or blobs such as images, text files, video and audio streams, large application data objects and documents, and virtual machine disk images. Objects are composed of the stored data, some metadata, and a unique ID for accessing the object. Object stores are designed to support files that are individually very large, as well provide large amounts of total storage to manage all files.  

![Example of object data](./images/object.png)

Some object data stores replicate a given blob across multiple server nodes enabling fast parallel reads of the data contained by the blob. This in turn enables the scale-out querying of data contained in large files because multiple processes, typically running on different servers, can each query the large data file simultaneously.  

One special case of object data stores is the network file share. Using file shares enables files to be accessed across a network using standard networking protocols like server message block (SMB). Given appropriate security and concurrent access control mechanisms, sharing data in this way can enable distributed services to provide highly scalable data access for performing basic, low level operations such as simple read and write requests.

Relevant Azure service:   
- [Azure Blob Storage](https://azure.microsoft.com/services/storage/blobs/)  
- [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/)  
- [Azure File Storage](https://azure.microsoft.com/services/storage/files/)  


### <a name="externalindexdata"></a> External index data stores
External index data stores provide the ability to search for information held in other data stores and services. External index data stores effectively provide a secondary index for any data store, and can be used to index massive volumes of data and provide near real-time access to these indexes. For example, in a file system the primary index used to uniquely identify a file is defined by the full path to the file. This makes searching for a file fast if you know its full path, but what if you want to search based on the contents of the file or some alternate metadata about the file? An external index lets you create these secondary search indexes and quickly retrieve the path to the files that match your criteria. Another example application of an external index is with key/value stores that only index the key for querying&mdash;if you have to be able to quickly query using data stored in the value, then you can build a secondary index on the value component of the data in an external index and use the result to return the key that uniquely identifies each matched item. 

![Example of search data](./images/search.png)

The key characteristics of a search engine database are the ability to store and index information very quickly, and provide fast response times for search requests. Indexes can be multidimensional and may support free-text searches across large volumes of text data. Indexing can be performed using a pull model, triggered by the search engine database, or using a push model, initiated by application code. 

External index data stores are often used to support full text and web based search. In these cases, searching can be exact or fuzzy. A fuzzy search finds documents that match a set of terms and calculates how closely they match. Some external indexes also support linguistic analysis that can return matches based on synonyms, genre expansions (for example, matching dogs to pets), and stemming (for example searching for run also matches ran and running). 

Relevant Azure service:  
- [Azure Search](https://azure.microsoft.com/services/search/)


<a name="requirements"></a>
### Typical requirements
Non-relational data stores often use a different storage architecture from that used by relational databases to address the requirements of the type of data they manage. Specifically, they tend towards having no fixed schema, thus enabling agility in evolving storage with the client application needs. Additionally, they tend not to support transactions (or they restrict the scope of transactions) and they generally don't include secondary indexes for scalability reasons.

The following compares the requirements for each of the non-relational data stores:<!--Colons aren't required in the first column, the table structure implies the relationship.-->

| Requirement | Document data | Column-family data | Key/value data | Graph data | Time series data | Object data | External index data |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Normalization | Denormalized | Denormalized | Denormalized | Normalized | Normalized | Denormalized | Denormalized |
| Schema | Schema on read | Column families defined on write, column schema on read | Schema on read | Schema on read | Schema on read | Schema on read | Schema on write | 
| Consistency (across concurrent transactions) | Tuneable consistency, document-level guarantees | Column-family&ndash;level guarantees | Key-level guarantees | Graph-level guarantees | N/A | N/A | N/A | 
| Referential Integrity | N/A | N/A | N/A | N/A | N/A | N/A | N/A |  
| Atomicity (transaction scope) | Collection | Table | Table | Graph | N/A | Object | N/A |
| Locking Strategy | Optmistic (lock free) | Pessimistic (row locks) | Optimistic (ETag) | Optmistic (lock free) | N/A | Pessimistic (blob locks) | N/A |
| Access pattern | Random access | Aggregates on tall/wide data | Random access | Random access | Random access and aggregation | Sequential access | Random access | 
| Indexing | Primary and secondary indexes | Primary and secondary indexes | Primary index only | Primary and secondary indexes | Primary and secondary indexes | Primary index only | N/A |
| Model | non-relational | non-relational | non-relational | non-relational | non-relational | non-relational | non-relational | 
| Data shape | Document | Tabular with column families containing columns | Key and value | Graph containing edges and vertices | Tabular | Blob and metadata | Document |
| Sparse | Yes | Yes | Yes | No | No | N/A | No | 
| Wide (lots of columns/attributes) | Yes | Yes | No | No | No | Yes | Yes |  
| Query interface | API or SQL | API or SQL | API | API | API | API | API | 
| Query flexibility (variety of access patterns supported) | Flexible | Flexible | Inflexible | Inflexible | Inflexible | Flexible |
| Datum size | Small (KBs) to medium (low MBs) | Medium (MBs) to Large (low GBs) | Small (KBs) | Small (KBs) | Small (KBs) | Large (GBs) to Very Large (TBs) | Small (KBs) |<!--I know it looks wrong, but it isn't. These aren't possessive or contractions.-->
| Overall Maximum Scale | Very Large (PBs) | Very Large (PBs) | Very Large (PBs) | Large (TBs) | Large (low TBs)  | Very Large (PBs) | Large (low TBs) | 


## <a name="wheretogo"></a>Where to go from here
Read next: Handling Unstructured Data Solution Pattern<!--This doesn't appear to exist.Did you want to link to the two patterns below? If so, they probably don't need to be repeated here.-->

See also: <!--These needed links. Some seem to map and others don't so I wasn't sure how you wanted them organized. I took my best guess. Also, actual titles of docs can be in title caps, everything else should be in sentence caps. Again, I did a little guessing here.-->

Related pipeline patterns 
- Handling unstructured data
    - [Processing CSV and JSON files](./processing-csv-and-json-files.md)
    - [Processing Free-form Text](./processing-free-form-text.md)
- [Handling Time Series Data](../pipeline-patterns/time-series.md)
    - Internet of Things
    - Real-time analytics

Related technology choices
- Handling unstructured data
    - [CSV and JSON file processing technology choices](../technology-choices/csv-json-options.md) 
    - Free-form text files
- [Time series solutions](../technology-choices/time-series.md)<!--I grabbed this link from another doc, but I don't see this doc?-->
    - Internet of Things
    - Real-time analytics
