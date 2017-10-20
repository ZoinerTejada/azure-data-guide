# Transactional Data 

**In this article**

[About]()

[When to use this data architecture](#whentouse)

[Benefits](#benefits)

[Challenges](#challenges)

[Best practices](#bestpractices)

[Where to go from here](#wheretogo)

<a name="about"></a>
The term transactional data refers to data describing an event, always having a time dimension, some numerical values and references to other data. Transactional data has very strong consistency requirements and the transactional data stores that support it leverage transactions using pessimistic locking to ensure all data are 100% consistent for all users and processes. 

Examples of typical transactions include: 
- e-commerce order management
- inventory
- accounting




## <a name="whentouse"></a>When to use this architecture

Transactional data tends to have the following requirements:

### Data Type Requirements
| Requirement | Description |
| --- | --- |
| Normalization: | Highly normalized |
| Schema: | Schema on write, strongly enforced|
| Consistency: | Strong consistency, ACID guarantees |
| Integrity: | High integrity |
| Uses Transactions: | Yes |
| Locking Strategy: | Pessimistic |
| Updateable: | Yes |
| Appendable: | Yes |
| Workload: | Heavy writes, moderate reads |
| Indexing: | Primary and secondary indexes |
| Datum size: | Small to medium sized |
| Data shape: | Tabular |
| Query flexibility: | Highly flexible |
| Scale: | Small (MB's) to Large (a few TB's) |

## <a name="benefits"></a>Benefits
TBD

## <a name="challenges"></a>Challenges
TBD

## <a name="bestpractices"></a>Best practices
TBD

## <a name="wheretogo"></a>Where to go from here
Related Common Architectures
- [Relational data stores](./relational-data-stores.md)
- Non-relational and No-SQL data stores

Related Solution Patterns
- Working with transactional data
    - [Online Transaction Processing (OLTP)](../solution-patterns/online-transaction-processing.md)
    - [Online Analytical Processing (OLAP)]()
    - [Data Warehousing]()

Related Technology Choices
- Transactional data stores
    - [Online Transaction Processing (OLTP) data stores](../technology-choices/oltp-data-stores.md)
    - [Online Analytical Processing (OLAP) data stores](../technology-choices/olap-data-stores.md)
    - [Data Warehouses](../technology-choices/data-warehouses.md)

