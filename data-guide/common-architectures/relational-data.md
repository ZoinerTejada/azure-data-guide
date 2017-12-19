# Relational data 

**In this article**

[About]()  
[Common Architectures](#common)   
[Where to go from here](#wheretogo)  

<a name="about"></a>
Relational data is data modeled using the relational model, whereby all data is expressed as tuples, and sets of tuples with the same headings form relations. A data store that organizes data using the relational model is referred to as a relational database. Relational databases use a tabular structure to materialize the relational model - that is they expose all the data as rows (tuples) in tables (relations). The database schema defines the columns (headings) of each table. Each column is defined with a name and a data type for all values stored in that column across all rows in the table.

![Example showing data using a relational database](./images/example-relational.png)

Most relational databases use the Structured Query Language (SQL) language that enables a  declarative approach to querying. The query author focuses solely on authoring a query that produces the desired result, allowing the relational database engine to decide how to actually execute the query. This is as opposed to using a procedural approach used by other data stores, whereby the query program specifies the processing steps explicitly.

Relational databases support several types of constraints, including:

- Primary key and unique constraints, that are used to uniquely identify rows within a table.
- Foreign key constraints that are created on a table to reference a row in another table by referencing the primary key or alternate key of the other table. Foreign key constraints are used in maintaining referential integrity, disallowing changes that would result in a mismatch in foreign key column values between referenced and referencing tables.
- Primary and secondary indexes. Primary indexes, which are used by the primary key, define the order of the data as it sits on disk. Secondary indexes provide an alternative combination of fields by which to quickly locate the desired rows, without having to re-sort the entire data on disk. The index structure used by relational databases typically includes B+ trees, R-trees and bitmaps.
- Check constraints, also known as entity integrity constraints, use expressions to define constraints that limit the values that can be stored within a single column, or in relationship to values in other columns of the same row.

Additionally, relational databases allow for the storage of executable code routines in the form of stored procedures and functions, which enable a mixture of declarative and procedural approaches.

The design of a relational database schema emphasizes minimizing the duplication of data through the use of [normal forms](https://en.wikipedia.org/wiki/Database_normalization#Normal_forms), a process also known as normalization, in order to prevent data anomalies and maintain data integrity. Relational databases are commonly designed to adhere to the [third normal form](https://en.wikipedia.org/wiki/Third_normal_form), though higher normal forms may be desired to gain additional benefits of normalization.

## <a name="common"></a> Common Architectures
The common architectures for relational data are:
- [Transactional Data](./transactional-data.md): predominantly used for write heavy scenarios such as order entry.
- [Semantic Modeling](./semantic-modeling.md): predominantly used for read heavy scenarios such as analytics and business intelligence.

## <a name="wheretogo"></a>Where to go from here
Read Next: [Transactional Data Common Architecture](./transactional-data.md)

See Also:

Related Common Architectures
- [Transactional Data](./transactional-data.md)
- [Semantic Modeling](./semantic-modeling.md)

Alternative Common Architectures
- [Non-relational and No-SQL common architectures](./non-relational-data.md)

Related Pipeline Patterns
- Working with transactional data
    - [Online Transaction Processing (OLTP)](../pipeline-patterns/online-transaction-processing.md)
    - [Online Analytical Processing (OLAP)](../pipeline-patterns/online-analytical-processing.md)
    - [Data Warehousing](../pipeline-patterns/data-warehousing.md)

Related Technology Choices
- Transactional data stores
    - [Online Transaction Processing (OLTP) data stores](../technology-choices/oltp-data-stores.md)
    - [Online Analytical Processing (OLAP) data stores](../technology-choices/olap-data-stores.md)
    - [Data Warehouses](../technology-choices/data-warehouses.md)