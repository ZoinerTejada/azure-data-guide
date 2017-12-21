# Transactional data 

**In this article**

[About]()  
[Typical Traits](#traits)  
[Best practices](#bestpractices)  
[Where to go from here](#wheretogo)  

<a name="about"></a>
Transactional data is information an organization collects that tracks the interactions related to what the organization does. These interactions are typically business transactions such as payments received from customers or payments made to suppliers, products moving through inventory, orders taken or services delivered. Transactional events, which represent the transactions themselves, not reference tables, typically contain a time dimension, some numerical values, and references to other data.

Transactional data stores that support strong consistency can leverage transactions using various locking strategies, such as pessimistic locking, to ensure all data are strongly consistent within the context of the enterprise, for all users and processes.

The most common deployment architecture that utilizes transactional data is the data store tier in a 3-tier architecture. A 3-tier architecture typically consists of a presentation tier, business logic tier, and data store tier. A related deployment architecture is the [N-tier](https://docs.microsoft.com/azure/architecture/guide/architecture-styles/n-tier) architecture, which may have multiple middle-tiers handling business logic.

![Example of a 3-tier application](./images/three-tier-application.png)

<a name="traits"></a>
### Typical Traits
Transactional data tends to have the following traits:

| Requirement | Description |
| --- | --- |
| Normalization | Highly normalized |
| Schema | Schema on write, strongly enforced|
| Consistency | Strong consistency, ACID guarantees |
| Integrity | High integrity |
| Uses transactions | Yes |
| Locking strategy | Pessimistic or Optimistic|
| Updateable | Yes |
| Appendable | Yes |
| Workload | Heavy writes, moderate reads |
| Indexing | Primary and secondary indexes |
| Datum size | Small to medium sized |
| Model | Relational |
| Data shape | Tabular |
| Query flexibility | Highly flexible |
| Scale | Small (MBs) to Large (a few TBs) | <!--I know it looks weird, but these are plural, not possessive or contractions.-->

## <a name="wheretogo"></a>Where to go from here

Read Next: [Online Transaction Processing (OLTP) Solution Pattern](../pipeline-patterns/online-transaction-processing.md)

See also:

Related common architectures
- [Relational data stores](./relational-data.md)

Alternative common architectures
- [Non-relational and No-SQL data stores](./non-relational-data.md)

Related pipeline patterns
- Working with transactional data
    - [Online Transaction Processing (OLTP)](../pipeline-patterns/online-transaction-processing.md)
    - [Online Analytical Processing (OLAP)](../pipeline-patterns/online-analytical-processing.md)
    - [Data Warehousing](../pipeline-patterns/data-warehousing.md)

Related technology choices
- Transactional data stores
    - [Online Transaction Processing (OLTP) data stores](../technology-choices/oltp-data-stores.md)
    - [Online Analytical Processing (OLAP) data stores](../technology-choices/olap-data-stores.md)
    - [Data Warehouses](../technology-choices/data-warehouses.md)

