# 13. Glossary of Key Terms

## **A**

- **ACID Properties**: A set of database transaction guarantees (Atomicity, Consistency, Isolation, Durability) ensuring reliable processing.
- **Aggregation**: The application of functions (SUM, AVG, COUNT, etc.) to grouped data to generate summary results.
- **ALTER**: A Data Definition Language (DDL) command that modifies the structure of database objects (e.g., adding or removing columns).
- **ANSI SQL-86**: The first standardized version of SQL, established in 1986, which played a key role in SQL’s adoption.
- **Apache Cassandra**: A distributed NoSQL wide-column database designed for high availability, scalability, and time-series data.
- **Atomicity**: An ACID property ensuring a transaction is treated as an indivisible unit—either all operations succeed or none do.
- **Azure Synapse Analytics**: Microsoft’s integrated analytics platform combining data warehousing and Big Data processing.

## **B**

- **BEGIN TRANSACTION**: A Transaction Control Language (TCL) command that initiates an explicit transaction in T-SQL.

## **C**

- **Clustered Index**: An index that dictates the physical storage order of table data; only one can exist per table.
- **Column (Field)**: A named data attribute in a table representing a specific type of information (e.g., Name, Age).
- **Columnstore Index**: A SQL Server index optimized for analytical queries by storing data column-wise.
- **COMMIT TRANSACTION**: A TCL command that finalizes a transaction, making its changes permanent.
- **Common Table Expression (CTE)**: A temporary named result set used within a single query (SELECT, INSERT, etc.).
- **Composite Primary Key**: A primary key composed of multiple columns, collectively ensuring row uniqueness.
- **Consistency**: An ACID property ensuring transactions transition the database between valid states, adhering to defined rules.
- **CREATE**: A DDL command used to generate new database objects (tables, views, indexes, etc.).
- **Cross Join**: A join type producing a Cartesian product—every row from one table paired with every row from another.

## **D**

- **DCL (Data Control Language)**: SQL commands (GRANT, REVOKE, DENY) managing user permissions and security.
- **DDL (Data Definition Language)**: SQL commands (CREATE, ALTER, DROP) defining and modifying database structures.
- **DELETE**: A Data Manipulation Language (DML) command removing specific rows from a table.
- **Deny Permissions**: A DCL command explicitly blocking a user/role from performing an action on a database object.
- **Distributed Database**: A database system where data is spread across multiple nodes for fault tolerance and scalability.
- **DML (Data Manipulation Language)**: SQL commands (INSERT, UPDATE, DELETE, MERGE) managing data within tables.
- **DQL (Data Query Language)**: SQL commands focused on data retrieval, primarily the SELECT statement.
- **DROP**: A DDL command permanently deleting a database object (e.g., DROP TABLE).
- **Durability**: An ACID property ensuring committed transactions persist despite system failures.
- **Dynamic Data Masking (DDM)**: A SQL Server feature that hides sensitive data in query results without altering stored data.

## **E**

- **E.F. Codd**: The computer scientist who pioneered the relational database model in the 1970s.
- **Execution Plan**: A roadmap showing how SQL Server retrieves data, used for query optimization.
- **Extended Events**: A SQL Server monitoring system for performance troubleshooting and diagnostics.

## **F**

- **Filtered Index**: A non-clustered index targeting a subset of data via a WHERE clause, reducing overhead.
- **Foreign Key**: A column referencing another table’s primary key, establishing a relationship.
- **Full-Text Index**: A specialized index enabling efficient text searches within string data.
- **Functions**: Reusable SQL routines returning a single value or table.

## **G**

- **GO**: A T-SQL batch separator indicating the end of a statement group.
- **Graph Database (e.g., Neo4j)**: A NoSQL database modeling data as nodes and edges for relationship-heavy datasets.
- **Grant Permissions**: A DCL command assigning access rights to users/roles.

## **H**

- **HAVING Clause**: Filters grouped data (after GROUP BY) based on aggregate conditions.
- **Hierarchical Database**: A tree-structured database model with parent-child relationships.

## **I**

- **IN**: A logical operator specifying multiple possible values for a column in a WHERE clause.
- **Indexing**: Creating lookup structures to speed up data retrieval.
- **INSERT**: A DML command adding new rows to a table.
- **Instance Configuration**: SQL Server setup step defining instance type (default/named) and directory paths.
- **Isolation**: An ACID property ensuring concurrent transactions operate independently to prevent conflicts.

## **J**

- **JSON Handling**: SQL Server capabilities for parsing, querying, and formatting JSON data.
- **JOIN**: Combines rows from multiple tables based on related columns.

## **K**

- **Key-Value Database (e.g., Redis)**: A NoSQL database storing data as key-value pairs for fast access.

## **L**

- **LIKE**: A pattern-matching operator in WHERE clauses.

## **M**

- **MERGE**: A DML "upsert" operation that inserts, updates, or deletes based on source-table comparisons.
- **Microsoft SQL Server**: A Microsoft-developed RDBMS with enterprise-grade features.
- **Mixed Mode Authentication**: SQL Server login method supporting both Windows and SQL Server authentication.
- **MongoDB**: A NoSQL document database storing flexible JSON-like records.
- **MySQL**: A popular open-source RDBMS for web applications.

## **N**

- **Neo4j**: A leading graph database platform.
- **Network Database**: A pre-relational model supporting many-to-many relationships (CODASYL standard).
- **Non-Clustered Index**: An index structure separate from data storage; multiple can exist per table.
- **NoSQL Database**: Non-relational databases optimized for unstructured/semi-structured data and scalability.

## **O**

- **Object-Oriented Database**: Stores data as objects with inheritance and polymorphism support.
- **Object Explorer**: The SSMS panel displaying database objects in a hierarchical view.
- **Oracle DB**: A high-performance RDBMS for large-scale enterprise use.
- **OUTPUT Clause**: Returns affected rows’ data (old/new values) after DML operations.
- **Over-indexing**: Excessive indexing that degrades write performance.

## **P**

- **PIVOT**: Transforms row data into aggregated columns.
- **PostgreSQL**: An extensible, standards-compliant open-source RDBMS.
- **Primary Key**: A column(s) uniquely identifying each table row.
- **Procedural Programming Capabilities**: T-SQL extensions like loops (WHILE), conditionals (IF), and error handling.

## **Q**

- **Query Optimizer**: SQL Server’s engine determining the most efficient query execution strategy.

## **R**

- **Relational Database (RDBMS)**: Organizes data into interrelated tables with keys.
- **Redis**: A high-performance key-value store.
- **REVOKE**: A DCL command removing previously assigned permissions.
- **Rollback Transaction**: A TCL command undoing all changes in a transaction.
- **Row (Record)**: A single data entry in a table.
- **Row-Level Security (RLS)**: Restricts row access based on user context.

## **S**

- **SA Account**: SQL Server’s default system administrator account with full privileges.
- **Savepoints**: Transaction markers allowing partial rollbacks.
- **Schema**: A logical container for database objects (tables, views, etc.).
- **SELECT**: Retrieves data from tables.
- **Server Configuration**: SQL Server installation phase setting up service accounts and startup options.
- **SQL (Structured Query Language)**: The standard language for relational database management.
- **SQL Server Management Studio (SSMS)**: Microsoft’s GUI tool for SQL Server administration.
- **Stored Procedure**: A precompiled SQL routine stored on the server.
- **Subqueries**: Nested queries supplying data to an outer query.
- **Sybase**: A company that co-developed early T-SQL with Microsoft.
- **System R**: IBM’s 1970s research project that influenced SQL’s development.

## **T**

- **Table**: A structured data set organized in rows and columns.
- **Table Designer**: The SSMS graphical interface for table creation/modification.
- **TCL (Transaction Control Language)**: Commands managing transactions (BEGIN, COMMIT, ROLLBACK).
- **Time-Series Database**: Optimized for timestamped data (e.g., IoT metrics).
- **Triggers**: Auto-executing procedures triggered by data changes (INSERT/UPDATE/DELETE).
- **TRUNCATE**: A DDL command rapidly deleting all table rows (non-logged).
- **TRY...CATCH**: T-SQL’s error-handling construct.
- **T-SQL (Transact-SQL)**: Microsoft’s SQL extension with procedural features.

## **U**

- **Under-indexing**: Insufficient indexing leading to slow queries.
- **UNPIVOT**: Converts columns into rows.
- **UPDATE**: Modifies existing table data.
- **User Account Control (UAC)**: A Windows security feature requiring admin approval for system changes.

## **V**

- **View**: A virtual table defined by a query (no independent data storage).

## **W**

- **WHERE Clause**: Filters rows in SELECT/UPDATE/DELETE statements.
- **Wide-Column Database (e.g., Apache Cassandra)**: A NoSQL type using flexible column families for scalability.
- **Window Functions**: Perform calculations across related rows without collapsing them into groups.
