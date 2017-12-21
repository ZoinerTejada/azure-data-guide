# Search Technology Choices

[About]()  
[What are your options when choosing a search data store?](#options)  
[How do you choose?](#howtochoose)  
[Key selection criteria](#criteria)  
[Capability matrix](#matrix)   
[Where to go from here](#wheretogo)  

<a name="about"></a>

## <a name="options"></a> What are your options when choosing a search data store?
In Azure, all of the following data stores will meet the core requirements for search against free-form text data by providing a search index:
- [Azure Search](https://docs.microsoft.com/azure/search/search-what-is-azure-search)
- [ElasticSearch](https://azuremarketplace.microsoft.com/marketplace/apps/elastic.elasticsearch?tab=Overview)
- [HDInsight with Solr](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-solr-install-linux)
- [SQL Server or Azure SQL Database with full text search](https://docs.microsoft.com/sql/relational-databases/search/full-text-search)

## <a name="howtochoose"></a> How do you choose?
Each data store brings with it a unique set of capabilities, giving you the option to select the one that most closely meets your requirements. 

## <a name="criteria"></a> Key selection criteria

The following table summarize the key differences in capabilities between each. <!--You might want to move this after the list. It may make more sense to introduce the questions, and then introduce the table with something like: "Based on your responses to the questions, the following table will help you select the choice that's right for you." or something along those lines. Also, BTW, this is one of the best decision making processes I've seen. Normally you get a table that tries to answer all the questions, but doesn't. Breaking it out this way is much easier to follow. -->For search scenarios, begin choosing the appropriate search data store for your needs by answering these questions:
- Do you want a managed service or do you prefer to setup and manage the cluster of virtual machines running the search data store?
    - If yes, then narrow your options to those that are managed services.
- Can you specify your index schema upfront?
    - If yes, then narrow your options to those that are schema on write.
- Do you need an index only for full-text search, or do you also need rapid aggregation of numeric data and other analytics?
    - If you need functionality beyond full-text search, then examine the options that support analytics beyond full text search.
- Do you need a search index for log analytics scenarios, that provides support for log collection, aggregation as well as visualizations on indexed data?
    - If yes, then you should consider the options that are part of a log analytics stack.
- Do you need support for semantic search such as identifying documents related to a given document or extracting the key phrases in a document?
    - If yes, consider the options that support semantic search.
- Do you need to index data in files on disk formats like plain text, PDF, Word, PowerPoint, and Excel?
    - If yes, consider the options that provide document indexers.
- Does your database have specific security needs?
    - If yes, examine the options that provide capabilities like transparent data encryption, authentication with Azure Active Directory and IP-based or virtual network&ndash;based access controls.

## <a name="matrix"></a> Capability matrix

### General capabilities
| | Azure Search | ElasticSearch | HDInsight with Solr | SQL Server or SQL DB with full text search | 
| --- | --- | --- | --- | --- | 
| Is managed service | Yes | No | Yes | Yes (for SQL DB and SQL Server managed instances) |  
| REST API | Yes | Yes | Yes | No |
| Programmability | .NET | Java | Java | T-SQL | 
| Document indexers for common file types (PDF, DOCX, TXT, and so on) | Yes | No | Yes | No |

### Manageability capabilities
| | Azure Search | ElasticSearch | HDInsight with Solr | SQL Server or SQL DB with full text search | 
| --- | --- | --- | --- | --- |
| Index schema definition | Schema fixed during creation | Updateable schema | Updateable schema | Updateable schema |
| Supports scale out  | Yes | Yes | Yes | No |

### Analytic workload capabilities
| | Azure Search | ElasticSearch | HDInsight with Solr | SQL Server or SQL DB with full text search | 
| --- | --- | --- | --- | --- | 
| Supports analytics beyond full text search | No | Yes | Yes | Yes |
| Part of a log analytics stack | No | Yes (ELK) <!--Term familiar to the audience-->|  No | No |
| Supports semantic search | Yes (find similar documents only) | Yes | Yes | Yes | 

### Security capabilities
| | Azure Search | ElasticSearch | HDInsight with Solr | SQL Server or SQL DB with full text search | 
| --- | --- | --- | --- | --- | 
| Row-level security | Partial (requires application query to filter by group id) | Partial (requires application query to filter by group id) | Yes | Yes | 
| Transparent data encryption | No | No | No | Yes |  
| Restrict access to specific IP addresses | No | Yes | Yes | Yes |   
| Restrict access to allow virtual network access only | No | Yes | Yes | Yes |  
| Active Directory authentication (integrated authentication) | No | No | No | Yes | 

## <a name="wheretogo"></a>Where to go from here
Read next: [Natural Language Processing Technology Choices](../technology-choices/natural-language-processing.md)

See also:

Related pipeline patterns
- Working with text data
    - [Processing CSV and JSON files](../pipeline-patterns/processing-csv-and-json.md)
    - [Processing free-form text data](../pipeline-patterns/processing-free-form-text.md)

