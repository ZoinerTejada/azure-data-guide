# Online Transaction Processing (OLTP) data stores

## What are your options when choosing an OLTP data store?
In Azure, all of the following data stores will meet the core requirements for OLTP and for the management of transaction data:
- Azure SQL Database
- Azure SQL Database Managed Instance
- SQL Server in Azure VM
- Azure Database for MySQL 
- Azure Database for PostgreSQL

## How do you choose?
Each data store brings with it a unique set of capabilities, giving you options in selecting the one that most closely meets your requirements. 

### Key Selection Criteria

The following table summarize the key differences in capabilities between each. For OLTP scenarios, being choosing the appropriate database for your needs by answering these questions:
- Do you want a managed service or do you prefer to manage the VM's running the database server?
    - If yes, then narrow your options to those that are managed services.
- Do you need a single database that supports more than 4TB?
    - If yes, then you will need one of the options that supports cluster scale-out.
- Does you application layer have specific dependencies for Microsoft SQL Server, MySQL or PostgreSQL compatibility?
    - Your application layer may limit the data stores you can choose based on the drivers it supports for communicating with the data store, or the assumptions it makes about which database is used.
- Are your write throughout requirements particularly high?
    - If yes, then you will want an option that provides in-memory tables that provide the fastest ingest of data that is not blocked by disk I/O.
- Is your solution multi-tenant?
    - If so, you might consider options that support capacity pools whereby multiple database instances draw from an elastic pool of resources, instead of fixed resources per database. This can help you better distribute capacity across all database instances, and can make your solution more cost effective.
- Does your database data need to be accessible with low latency in multiple geo-graphic regions? 
    - If yes, choose an option that supports readable secondaries. 
- Does your database need to be highly available across geo-graphic regions?
    - If yes, consider the options that provide support for geo-graphic replication. Also consider the options that support the automatic failover from the primary to the secondary.

### Capability Matrix

| | Azure SQL Database | Azure SQL Database Managed Instance | SQL Server in Azure VM| Azure Database for MySQL | Azure Database for PostgreSQL|
| --- | --- | --- | --- | --- | --- | 
| Is Managed Service | Yes | Yes | No | Yes | Yes |
| Max Data Size | 4 TB | 4 TB | 524 PB | 1 TB | 1 TB |
| JSON, XML and Spatial Data Support | Yes | Yes | Yes | Yes | Yes |
| Temporal tables | Yes | Yes | Yes | No | No |
| In-Memory Tables | Yes | Yes | Yes | No | No |
| Supports Capacity Pools  | Yes | No | No | No | No |
| Supports Clusters Scale Out  | No | No | Yes | No | No |
| Dynamic scalability (scale up)  | Yes | Yes | No | Yes | Yes |
| Rowstore Support | Yes | Yes | Yes | Yes | Yes | 
| Columnstore Support | Yes | Yes | Yes | No | No |
| Multiple Storage Engines | Yes | Yes | Yes | Yes | No| 
| In-Memory Columnstore Support | Yes | Yes | Yes | No | No |
| Adaptive Query Processing | Yes | Yes | Yes | No | No |
| Platforms | Windows | Windows | Windows, Linux, Docker | Linux | Linux |  
| Two-node High Availability | Yes | Yes | Yes | Yes | Yes | 
| Multi-node High Availability | Yes | Yes | Yes | Yes | Yes | 
| Supports Readable Secondaries | Yes | Yes | Yes | No | No | 
| Supports Geo-Graphic Replication | Yes | Yes | Yes | No | No | 
| Supports Automatic Failover to Secondary | Yes | No | No | No | No|
| Supports Point-in-time Restore | Yes | Yes | Yes | Yes | Yes |
| Row Level Security | Yes | Yes | Yes | Yes | Yes | 
| Data Masking | Yes | Yes | Yes | No | No |
| Transparent Data Encryption | Yes | Yes | Yes | Yes | Yes | 
| Restrict access to specific IP addresses | Yes | Yes | Yes | Yes | Yes |  
| Restrict access to allow VNET access only | Yes | Yes | Yes | No | No |  
| Active Directory authentication (integrated authentication) | Yes | Yes | Yes | No | No |
| Programmability | T-SQL, .NET | T-SQL, .NET, R, Python | T-SQL, .NET, R, Python | SQL | SQL |


