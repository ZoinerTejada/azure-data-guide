# Online Transaction Processing (OLTP)

[About]()  
[When to use this data architecture](#whentouse)  
[Benefits](#benefits)  
[Challenges](#challenges)  
[OLTP in Azure](#inazure)   
[Where to go from here](#wheretogo)  

<a name="about"></a>
The management of [transactional data](../common-architectures/transactional-data.md) using computer systems is referred to as Online Transaction Processing or OLTP. OLTP systems record the business interactions as they occur in the day-to-day operation of the organization, and support querying of this data to make inferences related to these business transactions.

## <a name="whentouse"></a>When to use this architecture
Choose OLTP when you have a data pipeline from source to data storage that needs to efficiently process and store business interactions and immediately make them available to client applications in a consistent way. Use this architecture when any tangible delay in processing would have a negative impact on the day-to-day operations of the business.

## <a name="benefits"></a>Benefits
OLTP systems are designed to efficiently process and store transactions, as well as query transactional data.

The goal of efficiently processing and storing individual transactions by an OLTP system is in part accomplished by data normalization - that is, breaking the data up into smaller chunks that are less redundant. This supports efficiency because it enables the OLTP system to process large numbers of transactions independently, and avoids extra processing needed to maintain data integrity in the presence of redundant data.

## <a name="challenges"></a>Challenges
Implementing and using an OLTP system can create a few challenges:

- OLTP systems are not always good for handling aggregates over large amounts of data, though there are exceptions to this, such as a well-planned SQL Server-based solution. Analytics against the data - that rely on aggregate calculations over millions of individual transactions - are very resource intensive for the OLTP system. They can be slow to execute and can cause a slow-down by blocking other transactions in the database. By extension, this affects the operations of the business.
- When conducting analytics and reporting on data stored in an OLTP system that is highly normalized, the queries used tend to be more complex, as most queries need to be constructed to de-normalize the data by using joins before it can be useful to the business. Additionally, naming conventions for database objects in OLTP systems tend to be terse and succinct. The increased normalization coupled with terse naming conventions makes OLTP systems difficult for business users attempting to query them for analytics purposes without the help of a DBA or data developer.
- Storing the history of transactions in perpetuity and storing too much data in any one table could lead to query performance issues, depending on the number of transactions stored. The common solution is to maintain a relevant window of time (such as the current fiscal year) in the OLTP system and offload historical data to other systems, such as a [datamart](./data-mart.md) or [data warehouse](./data-warehouse.md).

## <a name="inazure"></a>OLTP in Azure
Applications such as websites hosted in Azure Web Apps, REST APIs running within API Apps, or mobile or desktop applications communicate with the OLTP system (typically via a REST API intermediary).

In practice, most workloads are not purely OLTP - there tends to be an [analytical component](../pipeline-patterns/online-analytical-processing.md) to it as well. In addition, there is an increasing demand for real-time reporting, such as running reports against the operational system. This is also referred to as [HTAP (Hybrid Transactional and Analytical Processing)](../technology-choices/olap-data-stores.md#-what-are-your-options-when-choosing-an-olap-data-store).

![OLTP in Azure](./images/oltp-data-pipeline.png)

Related services:

- Data storage
    - [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/)
    - [SQL Server in an Azure VM](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview?toc=%2Fazure%2Fvirtual-machines%2Fwindows%2Ftoc.json)
    - [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/)
    - [Azure Database for PostgreSQL](https://docs.microsoft.com/azure/postgresql/)
- Data sources
    - [Web/API Apps](https://docs.microsoft.com/azure/app-service/)
    - [Mobile Apps](https://docs.microsoft.com/azure/app-service-mobile/)

## <a name="wheretogo"></a>Where to go from here
Read Next:
[Online Transaction Processing (OLTP) data store technology choices](../technology-choices/oltp-data-stores.md)

See Also:

Related Technology Choices
- Transactional data stores
    - [Online Transaction Processing (OLTP) data stores](../technology-choices/oltp-data-stores.md)
    - [Online Analytical Processing (OLAP) data stores](../technology-choices/olap-data-stores.md)
    - [Data Warehouses](../technology-choices/data-warehouses.md)