# Introduction to Indexes

- An index is an optional structure, associated with a table or table cluster, that can sometimes speed data access.

- Indexes are schema objects that are logically and physically independent of the data in the objects with which they are associated. 
- Thus, you can drop or create an index without physically affecting the indexed table.

**Note:

- If you drop an index, then applications still work. However, access of previously indexed data can be slower.

For an analogy, suppose an HR manager has a shelf of cardboard boxes.
Folders containing employee information are inserted randomly in the boxes. 
The folder for employee Whalen (ID 200) is 10 folders up from the bottom of box 1, whereas the folder for King (ID 100) is at the bottom of box 3.
To locate a folder, the manager looks at every folder in box 1 from bottom to top, and then moves from box to box until the folder is found.
To speed access, the manager could create an index that sequentially lists every employee ID with its folder location:

`ID 100: Box 3, position 1 (bottom)
ID 101: Box 7, position 8 
ID 200: Box 1, position 10
.
.
.
`

Similarly, the manager could create separate indexes for employee last names, department IDs, and so on.

The absence or presence of an index does not require a change in the wording of any SQL statement.

An index is a fast access path to a single row of data. It affects only the speed of execution. Given a data value that has been indexed, the index points directly to the location of the rows containing that value.

When an index exists on one or more columns of a table, the database can in some cases retrieve a small set of randomly distributed rows from the table. Indexes are one of many means of reducing disk I/O. If a heap-organized table has no indexes, then the database must perform a full table scan to find a value. For example, a query of location 2700 in the unindexed hr.departments table requires the database to search every row in every block. This approach does not scale well as data volumes increase.

Disadvantages of indexes include the following:

   - Creating indexes manually often requires deep knowledge of the data model, application, and data distribution.

   - As the data changes, you must revisit previous decisions about indexes. An index might stop being useful, or new indexes might be required.

    - Indexes occupy disk space.

    - The database must update the index when DML occurs on the indexed data, which creates performance overhead.

Note:

> Starting in Oracle Database 19c, Oracle Database can constantly monitor the application workload, creating and managing indexes automatically. Automated indexing is implemented as a database task that runs at a fixed interval.

Consider creating an index in the following situations:

    The indexed columns are queried frequently and return a small percentage of the total number of rows in the table.

    A referential integrity constraint exists on the indexed column or columns. The index is a means to avoid a full table lock that would otherwise be required if you update the parent table primary key, merge into the parent table, or delete from the parent table.

    A unique key constraint will be placed on the table and you want to manually specify the index and all index options.

Index Usability and Visibility

Indexes are usable (default) or unusable, visible (default) or invisible.
Keys and Columns

A key is a set of columns or expressions on which you can build an index.

Although the terms are often used interchangeably, indexes and keys are different. Indexes are structures stored in the database that users manage using SQL statements. Keys are strictly a logical concept.

The following statement creates an index on the customer_id column of the sample table oe.orders:

CREATE INDEX ord_customer_ix ON orders (customer_id);

In the preceding statement, the customer_id column is the index key. The index itself is named ord_customer_ix.

Composite Indexes

A composite index, also called a concatenated index, is an index on multiple columns in a table.

Place columns in a composite index in the order that makes the most sense for the queries that will retrieve data. The columns need not be adjacent in the table.

Composite indexes can speed retrieval of data for SELECT statements in which the WHERE clause references all or the leading portion of the columns in the composite index. Therefore, the order of the columns used in the definition is important. In general, the most commonly accessed columns go first.

For example, suppose an application frequently queries the last_name, job_id, and salary columns in the employees table. Also assume that last_name has high cardinality, which means that the number of distinct values is large compared to the number of table rows. You create an index with the following column order:

CREATE INDEX employees_ix
   ON employees (last_name, job_id, salary);

Queries that access all three columns, only the last_name column, or only the last_name and job_id columns use this index. In this example, queries that do not access the last_name column do not use the index.

Note:

In some cases, such as when the leading column has very low cardinality, the database may use a skip scan of this index (see "Index Skip Scan").

For example, a nonpartitioned index, global partitioned index, and locally partitioned index can exist for the same table columns in the same order. Only one index with the same number of columns in the same order can be visible at any one time.

This capability enables you to migrate applications without the need to drop an existing index and re-create it with different attributes. Also, this capability is useful in an OLTP database when an index key keeps increasing, causing the database to insert new entries into the same set of index blocks. To alleviate such "hot spots," you could evolve the index from a nonpartitioned index into a global partitioned index.

If indexes on the same set of columns do not differ in type or partitioning scheme, then these indexes must use different column permutations. For example, the following SQL statements specify valid column permutations:
CREATE INDEX employee_idx1 ON employees (last_name, job_id);
CREATE INDEX employee_idx2 ON employees (job_id, last_name);

Unique and Non-unique Indexes

Indexes can be unique or nonunique. Unique indexes guarantee that no two rows of a table have duplicate values in the key column or columns.

For example, your application may require that no two employees have the same employee ID. In a unique index, one rowid exists for each data value. The data in the leaf blocks is sorted only by key.

Nonunique indexes permit duplicates values in the indexed column or columns. For example, the first_name column of the employees table may contain multiple Mike values. For a nonunique index, the rowid is included in the key in sorted order, so nonunique indexes are sorted by the index key and rowid (ascending).

Oracle Database does not index table rows in which all key columns are null, except for bitmap indexes or when the cluster key column value is null.
Types of Indexes

Oracle Database provides several indexing schemes, which provide complementary performance functionality.

B-tree indexes are the standard index type. They are excellent for highly selective indexes (few rows correspond to each index entry) and primary key indexes. Used as concatenated indexes, a B-tree index can retrieve data sorted by the indexed columns. B-tree indexes have the subtypes shown in the following table.
