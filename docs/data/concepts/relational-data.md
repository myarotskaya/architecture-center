---
title: Relational data
description: 
author: zoinerTejada
ms:date: 01/17/2018
---

# Relational data

Relational data is data modeled using the relational model. In this model, data is expressed as tuples. A *tuple* is a set of attribute/value pairs. For example, a tuple might be (itemid = 5, orderid = 1, item = "Chair", amount = 200.00). A set of tuples that all share the same attributes is called a *relation*. 

Relations are naturally represented as tables, where each tuple is exposed as a row in the table. However, rows have an explicit ordering, unlike tuples. The database schema defines the columns (headings) of each table. Each column is defined with a name and a data type for all values stored in that column across all rows in the table.

![Example showing data using a relational database](./images/example-relational.png)

A data store that organizes data using the relational model is referred to as a relational database. Primary keys uniquely identify rows within a table. Foreign key fields are used in one table to refer to a row in another table by referencing the primary key of other table. Foreign keys are used in maintaining referential integrity, ensuring that the referenced rows are not altered or deleted while the referencing row depends on them. 

![Example showing data using a relational database](./images/example-relational2.png)

Relational databases support varying forms of constraints that help to ensure data integrity:

- Unique constraints ensure that all values in a column are unique. 

- Foreign key constraints enforce a link between the data in two tables. A foreign key references the primary key or another unique key from another table. A foreign key constraint enforces referential integrity, disallowing changes that cause invalid foreign key values.

- Check constraints, also known as entity integrity constraints, limit the values that can be stored within a single column, or in relationship to values in other columns of the same row. 

Most relational databases use the Structured Query Language (SQL) language that enables a  declarative approach to querying. The query author focuses solely on authoring a query that shapes the desired result, allowing the relational database engine to decide how to actually execute the query. This is as opposed to the procedural approach used by other data stores, whereby the query program specifies the processing steps explicitly. Relational databases also allow for the storage of executable code routines in the form of stored procedures and functions, which enable a mixture of declarative and procedural approaches.

To improve query performace, relational databases use *indexes*. Primary indexes, which are used by the primary key, define the order of the data as it sits on disk. Secondary indexes provide an alternative combination of fields by which to quickly locate the desired rows, without having to re-sort the entire data on disk. The index structure used by relational databases typically includes B+ trees, R-trees and bitmaps.

Because relational databases enforce referential integrity, scaling a relational database can become challenging. You can scale out the database by sharding the data, but this requires careful design of the schema. For more information, see [Sharding pattern](../../patterns/sharding.md).

If data is non-relational or has requirements that are not suited to a relational database, consider a [Non-relational or NoSQL](./non-relational-data.md)data store.
