# Online Transaction Processing (OLTP) data stores

[About]()  
[What are your options when choosing an OLTP data store?](#options)  
[How do you choose?](#howtochoose)  
[Key selection criteria](#criteria)  
[Capability matrix](#matrix)   
[Where to go from here](#wheretogo)  

<a name="about"></a>

## <a name="options"></a> What are your options when choosing an OLTP data store?
In Azure, all of the following data stores will meet the core requirements for OLTP and for the management of transaction data:
- Azure SQL Database
- Azure SQL Database Managed Instance
- SQL Server in an Azure virtual machine
- Azure Database for MySQL 
- Azure Database for PostgreSQL

## <a name="howtochoose"></a> How do you choose?
Each data store brings with it a unique set of capabilities, giving you the option to select the one that most closely meets your requirements. 

## <a name="criteria"></a> Key selection criteria

The table below summarizes the key differences in capabilities between each. <!--You might want to move this after the list. It may make more sense to introduce the questions, and then introduce the table with something like: "Based on your responses to the questions, the following table will help you select the choice that's right for you." or something along those lines. Also, BTW, this is one of the best decision making processes I've seen. Normally you get a table that tries to answer all the questions, but doesn't. Breaking it out this way is much easier to follow. -->For OLTP scenarios, begin choosing the appropriate database for your needs by answering these questions:
- Do you want a managed service or do you prefer to manage the virtual machines running the database server?
    - If yes, then narrow your options to those that are managed services.
- Do you need a single database that supports more than 4 TB?
    - If yes, then you will need one of the options that support cluster scale out.
- Does you application layer have specific dependencies for Microsoft SQL Server, MySQL, or PostgreSQL compatibility?
    - Your application layer may limit the data stores you can choose based on the drivers it supports for communicating with the data store, or the assumptions it makes about which database is used.
- Are your write throughput requirements particularly high?
    - If yes, then you will want an option that provides in-memory tables that provide the fastest ingest of data that is not blocked by disk I/O.
- Is your solution multi-tenant?
    - If so, you might consider options that support capacity pools whereby multiple database instances draw from an elastic pool of resources, instead of fixed resources per database. This can help you distribute capacity better across all database instances, and can make your solution more cost effective.
- Does your database data need to be accessible with low latency in multiple geographic regions? 
    - If yes, choose an option that supports readable secondaries. 
- Does your database need to be highly available across geographic regions?
    - If yes, consider the options that provide support for geographic replication. Also consider the options that support automatic failover from the primary to the secondary.
- Does your database have specific security needs?
    - If yes, examine the options that provide capabilities like row level security, data masking, and transparent data encryption.

## <a name="matrix"></a> Capability matrix

### General capabilities 
| | Azure SQL Database | Azure SQL Database managed instance | SQL Server in an Azure virtual machine| Azure Database for MySQL | Azure Database for PostgreSQL|<!--We're not supposed to abbreviate virtual machine. It may be better to say: Azure virtual machine with SQL Server or something else. I just spelled out and made it grammatical.-->
| --- | --- | --- | --- | --- | --- | 
| Is managed service | Yes | Yes | No | Yes | Yes |
| Runs on platform | Windows | Windows | Windows, Linux, Docker | Linux | Linux |  
| JSON, XML, and spatial data support | Yes | Yes | Yes | Yes | Yes |
| Programmability | T-SQL, .NET, R | T-SQL, .NET, R, Python | T-SQL, .NET, R, Python | SQL | SQL |

### Scalability capabilities
| | Azure SQL Database | Azure SQL Database managed instance | SQL Server in an Azure virtual machine| Azure Database for MySQL | Azure Database for PostgreSQL|
| --- | --- | --- | --- | --- | --- | 
| Max data size | 4 TB | 35 TB | 256 TB | 1 TB | 1 TB |
| Supports capacity ools  | Yes | No | No | No | No |
| Supports cluster scale out  | No | No | Yes | No | No |
| Dynamic scalability (scale up)  | Yes | Yes | No | Yes | Yes |

### Analytic workload capabilities
| | Azure SQL Database | Azure SQL Database managed instance | SQL Server in an Azure virtual machine| Azure Database for MySQL | Azure Database for PostgreSQL|
| --- | --- | --- | --- | --- | --- | 
| Temporal tables | Yes | Yes | Yes | No | No |
| In-memory Tables | Yes | Yes | Yes | No | No |
| Columnstore support | Yes | Yes | Yes | No | No |
| In-memory columnstore support | Yes | Yes | Yes | No | No |
| Multiple storage engines | Yes | Yes | Yes | Yes | No| 
| Adaptive query processing | Yes | Yes | Yes | No | No |


### Availability capabilities
| | Azure SQL Database | Azure SQL Database managed instance | SQL Server in an Azure virtual machine| Azure Database for MySQL | Azure Database for PostgreSQL|
| --- | --- | --- | --- | --- | --- | 
| Supports readable secondaries | Yes | Yes | Yes | No | No | 
| Supports geographic replication | Yes | Yes | Yes | No | No | 
| Supports automatic failover to secondary | Yes | No | No | No | No|
| Supports point-in-time restore | Yes | Yes | Yes | Yes | Yes |


### Security capabilities
| | Azure SQL Database | Azure SQL Database managed instance | SQL Server in an Azure virtual machine| Azure Database for MySQL | Azure Database for PostgreSQL|
| --- | --- | --- | --- | --- | --- | 
| Row level security | Yes | Yes | Yes | Yes | Yes | 
| Data masking | Yes | Yes | Yes | No | No |
| Transparent data encryption | Yes | Yes | Yes | Yes | Yes | 
| Restrict access to specific IP addresses | Yes | Yes | Yes | Yes | Yes |  
| Restrict access to allow virtual network access only | Yes | Yes | Yes | No | No |  
| Active Directory authentication (integrated authentication) | Yes | Yes | Yes | No | No |

## <a name="wheretogo"></a>Where to go from here
Read next:
 [Data Warehousing Solution Pattern](../pipeline-patterns/data-warehousing.md)

See also:

Related pipeline patterns
- Working with transactional data
    - [Online Transaction Processing (OLTP)](../pipeline-patterns/online-transaction-processing.md)
    - Online Analytical Processing (OLAP)
    - Data Warehousing

Related technology choices
- Transactional data stores
    - [Online Analytical Processing (OLAP) data stores](../technology-choices/olap-data-stores.md)
    - [Data Warehouses](../technology-choices/data-warehouses.md)
    - [Data serving storage](../technology-choices/data-serving-storage.md)
