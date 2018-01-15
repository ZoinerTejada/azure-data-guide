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
- [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/)
- Azure SQL Database Managed Instance
- [SQL Server in an Azure virtual machine](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview?toc=%2Fazure%2Fvirtual-machines%2Fwindows%2Ftoc.json)
- [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/)
- [Azure Database for PostgreSQL](https://docs.microsoft.com/azure/postgresql/)

## <a name="howtochoose"></a> How do you choose?
Each data store brings with it a unique set of capabilities, giving you the option to select the one that most closely meets your requirements. 

## <a name="criteria"></a> Key selection criteria

The following table summarize the key differences in capabilities between each option. For the OLTP scenarios, begin choosing the appropriate database for your needs by answering these questions:

- Do you want a managed service, or do you prefer to manage the VMs running the database server?
    - Managed services, typically PaaS-based, removes the operational overhead required by Infrastructure-as-a-Service (IaaS) virtual machines, such as patching, configuring high availability, and applying the security best practices associated with managing a server. However, if you do need to use an IaaS-based solution, consider using one of the database images on [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/) and use automated patching and backup on your provisioned VMs to reduce the administrative burden. Otherwise, narrow your options to those that are managed services.
- Does your solution have specific dependencies for Microsoft SQL Server, MySQL or PostgreSQL compatibility?
    - Your application may limit the data stores you can choose based on the drivers it supports for communicating with the data store, or the assumptions it makes about which database is used.
- Are your write throughput requirements particularly high?
    - If yes, then you will want an option that provides in-memory tables that provide the fastest ingest of data that is not blocked by disk I/O, as long as the data is able to fit in memory.
- Is your solution multi-tenant?
    - If so, you might consider options that support capacity pools whereby multiple database instances draw from an elastic pool of resources, instead of fixed resources per database. This can help you better distribute capacity across all database instances, and can make your solution more cost effective.
- Does your database data need to be accessible with low latency in multiple geo-graphic regions? ]
    - If yes, choose an option that supports readable secondaries.
- Does your database need to be highly available across geo-graphic regions?
    - If yes, consider the options that provide support for geo-graphic replication. Also consider the options that support the automatic failover from the primary to the secondary.
- Does your database have specific security needs?
    - If yes, examine the options that provide capabilities like row level security, data masking, and transparent data encryption.

## <a name="matrix"></a> Capability matrix

### General capabilities 
| | Azure SQL Database | Azure SQL Database managed instance | SQL Server in an Azure virtual machine | Azure Database for MySQL | Azure Database for PostgreSQL |
| --- | --- | --- | --- | --- | --- |
| Is Managed Service | Yes | Yes | No | Yes | Yes |
| Runs on Platform | N/A | N/A | Windows, Linux, Docker | N/A | N/A |
| JSON, XML and Spatial Data Support | Yes | Yes | Yes | Yes | Yes |
| Programmability \* | T-SQL, .NET, R | T-SQL, .NET, R, Python | T-SQL, .NET, R, Python | SQL | SQL |

\* Excludes client driver support, which allows many programming languages to connect to and use the OLTP data store.

### Scalability capabilities
| | Azure SQL Database | Azure SQL Database Managed Instance | SQL Server in an Azure virtual machine| Azure Database for MySQL | Azure Database for PostgreSQL|
| --- | --- | --- | --- | --- | --- |
| Max database instance size | [4 TB](https://docs.microsoft.com/azure/sql-database/sql-database-resource-limits) | 4 TB | 256 TB | [1 TB](https://docs.microsoft.com/azure/mysql/concepts-limits) | [1 TB](https://docs.microsoft.com/azure/postgresql/concepts-limits) |
| Supports capacity pools  | Yes | Yes | Yes | No | No |
| Supports clusters scale out  | No | No | Yes | No | No |
| Dynamic scalability (scale up)  | Yes | Yes | No | Yes | Yes |

### Analytic workload capabilities
| | Azure SQL Database | Azure SQL Database managed instance | SQL Server in an Azure virtual machine| Azure Database for MySQL | Azure Database for PostgreSQL|
| --- | --- | --- | --- | --- | --- | 
| Temporal tables | Yes | Yes | Yes | No | No |
| In-memory (memory-optimized) tables | Yes | Yes | Yes | No | No |
| Columnstore support | Yes | Yes | Yes | No | No |
| Adaptive query processing | Yes | Yes | Yes | No | No |

### Availability capabilities
| | Azure SQL Database | Azure SQL Database Managed Instance | SQL Server in an Azure virtual machine| Azure Database for MySQL | Azure Database for PostgreSQL|
| --- | --- | --- | --- | --- | --- | 
| Supports readable secondaries | Yes | Yes | Yes | No | No | 
| Supports geographic replication | Yes | Yes | Yes | No | No | 
| Supports automatic failover to secondary | Yes | No | No | No | No|
| Supports point-in-time restore | Yes | Yes | Yes | Yes | Yes |

### Security capabilities
| | Azure SQL Database | Azure SQL Database Managed Instance | SQL Server in an Azure virtual machine| Azure Database for MySQL | Azure Database for PostgreSQL|
| --- | --- | --- | --- | --- | --- | 
| Row level security | Yes | Yes | Yes | Yes | Yes |
| Data masking | Yes | Yes | Yes | No | No |
| Transparent data encryption | Yes | Yes | Yes | Yes | Yes |
| Restrict access to specific IP addresses | Yes | Yes | Yes | Yes | Yes |
| Restrict access to allow VNET access only | Yes | Yes | Yes | No | No |
| Azure Active Directory authentication | Yes | Yes | Yes | No | No |
| Active Directory authentication | No | No | Yes | No | No |
| Multi-factor authentication | Yes | Yes | Yes | No | No |
| [Always Encrypted](https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-database-engine) | Yes | Yes | Yes | No | No |
| Private IP | No | Yes | Yes | No | No |

## <a name="wheretogo"></a>Where to go from here
Read next:
 [Data Warehousing Pipeline Pattern](../pipeline-patterns/data-warehousing.md)

See also:

Related pipeline patterns
- Working with transactional data
    - [Online Transaction Processing (OLTP)](../pipeline-patterns/online-transaction-processing.md)
    - [Online Analytical Processing (OLAP)](../pipeline-patterns/online-analytical-processing.md)
    - [Data Warehousing](../pipeline-patterns/data-warehousing.md)

Related technology choices
- Transactional data stores
    - [Online Analytical Processing (OLAP) data stores](../technology-choices/olap-data-stores.md)
    - [Data Warehouses](../technology-choices/data-warehouses.md)
    - [Data serving storage](../technology-choices/data-serving-storage.md)
