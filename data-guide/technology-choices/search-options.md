# Search Technology Choices

[About]()  
[What are your options when choosing a search data store?](#options)  
[How do you choose?](#howtochoose)  
[Key Selection Criteria](#criteria)  
[Capability Matrix](#matrix)   
[Where to go from here](#wheretogo)  

<a name="about"></a>

## <a name="options"></a> What are your options when choosing a search data store?
In Azure, all of the following data stores will meet the core requirements for search against free-form text data by providing a search index:
- Azure Search
- HDInsight with Solr
- SQL Server or Azure SQL Database with Full Text Search

## <a name="howtochoose"></a> How do you choose?
Each data store brings with it a unique set of capabilities, giving you options in selecting the one that most closely meets your requirements. 

## <a name="criteria"></a> Key Selection Criteria

The following table summarize the key differences in capabilities between each. For search scenarios, begin choosing the appropriate search data store for your needs by answering these questions:
- Do you want a managed service or do you prefer to setup and manage the cluster of VM's running the search data store?
    - If yes, then narrow your options to those that are managed services.
- Can you specify your index schema upfront?
    - If yes, then narrow your options to those that are schema on write.
- Do you need an index only for full-text search, or do you also need rapid aggregation of numeric data and other analytics?
    - If you need functionality beyond full-text search, then examine the options that supports analytics beyond full text search.
- Do you need a search index for log analytics scenarios, that provides support for log collection, aggregation as well as visualizations on indexed data?
    - If yes, then you should consider the options that are part of a log analytics stack.
- Do you need support for semantic search such as identifying documents related to a given document or extracting the key phrases in a document?
    - If yes, consider the options that support semantic search.
- Do you need to index data in files on disk formats like plain text, PDF, Word, PowerPoint and Excel?
    - If yes, consider the options that provide document indexers.
- Does your database have specific security needs?
    - If yes, examine the options that provide capabilities like Transparent Data Encryption, authentication with Azure Active Directory and IP based or VNET based access controls.

## <a name="matrix"></a> Capability Matrix

### General Capabilities
| | Azure Search | ElasticSearch | HDInsight with Solr | SQL Server or SQL DB with Full Text Search | 
| --- | --- | --- | --- | --- | --- | 
| Is Managed Service | Yes | No | Yes | Yes (for SQL DB and SQL Server Managed Instances) |  
| REST API | Yes | Yes | Yes | No |
| Programmability | .NET | Java | Java | T-SQL | 
| Document indexers for common file types (PDF, DOCX, TXT, etc.) | Yes | No | Yes | No |

### Manageability Capabilities
| | Azure Search | ElasticSearch | HDInsight with Solr | SQL Server or SQL DB with Full Text Search | 
| --- | --- | --- | --- | --- | --- | 
| Index Schema Definition | Schema fixed during creation | Updateable schema | Updateable schema | Updateable schema |
| Supports Scale Out  | Yes | Yes | Yes | No |

### Analytic Workload Capabilities
| | Azure Search | ElasticSearch | HDInsight with Solr | SQL Server or SQL DB with Full Text Search | 
| --- | --- | --- | --- | --- | --- | 
| Supports analytics beyond full text search | No | Yes | Yes | Yes |
| Part of a log analytics stack | No | Yes (ELK) |  No | No |
| Supports semantic search | Yes (find similar documents only) | Yes | Yes | Yes | 

### Security Capabilities
| | Azure Search | ElasticSearch | HDInsight with Solr | SQL Server or SQL DB with Full Text Search | 
| --- | --- | --- | --- | --- | --- | 
| Row Level Security | Partial (requires application query to filter by group id) | Partial (requires application query to filter by group id) | Yes | Yes | 
| Transparent Data Encryption | No | No | No | Yes |  
| Restrict access to specific IP addresses | No | Yes | Yes | Yes |   
| Restrict access to allow VNET access only | No | Yes | Yes | Yes |  
| Active Directory authentication (integrated authentication) | No | No | No | Yes | 

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
