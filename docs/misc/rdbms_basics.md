# RDBMS Basics

Here at Skit, we heavily leverage relational databases to persist information flowing through our services.

This document is to give a quick grasp of the concepts that we make use of the most when using these systems.

This doc should not be considered the definitive guide to understanding about RDBMS systems. For that, we'd suggest 
going through [this][1] or [this][2].

## A table and all it entails

In an RDBMS(Relational Database Management System), all the information is generally stored in a table. We attempt to 
capture the different properties of such RDBMS tables below:

| Property    | Description                                                                                        |
|-------------|----------------------------------------------------------------------------------------------------|
| Column      | Each column represents a property  of the data being stored.   Columns are also called attributes. |
| Row         | Each row represents a record of data. A single row is called a tuple.                              |
| Schema      | Represents different tables in a DB and  their relationship with each other.                       |
| Cardinality | Number of rows present in a table.                                                                 |

If the above table were to be converted into an RDBMS table, it would have the following properties:

* Has 2 columns/attributes(Property, Description).
* Has a cardinality of 4. i.e. 4 rows
* Each tuple contains 2 properties. i.e. columns

## Constraints

These are conditions applicable to the columns of a table which decide whether the data being inserted/updated is valid 
or not. Constraints can either be at table level or column level.

Column level constraints only govern the data that's inserted/updated as a part of that column. Table level constrains 
are applicable to all the columns in the table. 
(a deeper dive can be found [here][3])

## Normalization

It is the process of organizing data efficiently in the database. This is to ensure that there is:

1. No Data redundancy: Same data is not repeated repeated across tables.
2. Data dependency: Data is organized in the way it is dependent on other data. 

To read more on the topic, we'd suggest going through [1-NF][4], [2-NF][5] and [3-NF][6] normalization forms which are guidelines to 
formalize the rules of normalization.

## Indexing

This is one of the most important concepts you will use when dealing with large datasets like we do here at Skit.

Indexes are a technique to efficiently retrieve data from a DBMS system on the basis of some properties. As your 
tables increase in size, accessing those records becomes slower. This is where indexes come to your rescue.

The types of indexes generally available are:

| Index Type       | Description                                                                                                                                         |
|------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| Primary Index    | Defined on the primary key of the table.                                                                                                            |
| Secondary Index  | Defined on keys other than the primary key. Can be used to both unique and non-unique columns.                                                      |
| Clustering Index | Defines the order in which data is physically stored. Since this data can only be ordered in 1 way, there can only be 1 clustering index per table. |

Indexes are usually built using columns which are commonly used to retrieve records. That's when they're most useful.

If an index is built using a given column, said column is referred to as an _indexed column_.
Using SQL queries with indexed columns in `where` clauses causes the index to be used. 
This results in faster retrieval of records.

Non-indexed columns are searched using a sequential scan. i.e. a scan of all the values of that column in the table 
till the matching values are found. As is obvious, this is the most sub-optimal way of fetching records.

The primary and clustering indexes are based on ordered data. Ordered indexes can be further sub-divided into the following types:

| Index Type   | Description                                                                                                                                                                                                                                                                                                                          |
|--------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Dense Index  | Creates an index record for every search key value in the table. This makes searching faster but requires more space to store the index.                                                                                                                                                                                             |
| Sparse Index | Creates an index record only certain search keys. Usual practice is to use equally distributed search keys so as to get most benefit from sparse indexes.  If a key is not present at the nearest index, a sequential scan starts from that point to locate the record. This makes searching slightly slower but optimizes on space. | 

## Conclusion

We hope this document served as a nice primer on the features of an RDBMS system. These should help mould the decisions 
you make regarding database schemas and how to optimise those records for retrieval.

[1]: https://www.tutorialspoint.com/sql/sql-rdbms-concepts.htm
[2]: https://www.javatpoint.com/what-is-rdbms
[3]: https://www.tutorialspoint.com/sql/sql-constraints.htm
[4]: https://www.tutorialspoint.com/sql/first-normal-form.htm
[5]: https://www.tutorialspoint.com/sql/second-normal-form.htm
[6]: https://www.tutorialspoint.com/sql/third-normal-form.htm
