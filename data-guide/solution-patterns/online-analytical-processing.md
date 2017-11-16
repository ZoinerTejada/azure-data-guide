# Online Analytical Processing

[About]()  
[When to use this data architecture](#whentouse)  
[Benefits](#benefits)  
[Challenges](#challenges)  
[OLAP in Azure](#inazure)   
[Where to go from here](#wheretogo)  

<a name="about"></a>
The databases that a business uses to store all its transactions and records are called [online transaction processing (OLTP)](online-transaction-processing.md) databases. These databases usually have records that are entered one at a time and that contain a wealth of information that can be used by strategists to make informed decisions about their business. The databases that are used to store the data, however, were not designed for analysis. Therefore, retrieving answers from these databases is costly in terms of time and effort. Online analytical processing (OLAP) systems were designed to help extract this business intelligence information from the data in a highly performant way. This is because OLAP databases are optimized for heavy read, low write operations.

## <a name="whentouse"></a>When to use this architecture

Choose OLAP when you need to rapidly execute complex analytical and ad hoc queries without negatively impacting your OLTP systems trying to conduct other transactions. Also consider using this architecture when you want to provide business users with a simple way to generate reports off your data, without them needing to know how to work with the underlying data relationships, figure out naming conventions, and when you want to provide a number of aggregations that will allow them to have fast, consistent results. OLAP really shines when you want to apply aggregate calculations over large amounts of data.

## <a name="benefits"></a>Benefits

OLAP systems are optimized for read heavy scenarios, such as analytics and business intelligence.

OLAP allows business users to slice and dice data as needed, regardless of whether the source data is partitioned across several data sources. The semantic models business users can use help abstract relationship complexities and make it easier to analyze the data much faster than they'd be able to otherwise, if at all.

## <a name="challenges"></a>Challenges



## <a name="inazure"></a>OLAP in Azure


## <a name="wheretogo"></a>Where to go from here
Read Next:
[Online Analytical Processing (OLAP) data store technology choices](../technology-choices/olap-data-stores.md)

See Also:

Related Technology Choices
- Transactional data stores
    - [Online Transaction Processing (OLTP) data stores](../technology-choices/oltp-data-stores.md)
    - [Online Analytical Processing (OLAP) data stores](../technology-choices/olap-data-stores.md)
    - [Data Warehouses](../technology-choices/data-warehouses.md)