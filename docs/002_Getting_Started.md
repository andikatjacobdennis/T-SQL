# 002. Getting Started

## Datum

- A datum (plural: data) is a single piece of information. It represents the most basic unit of data.
- Example "42" is a datum representing a person's age.

  | Age |
  | --- |
  | 42  |

## Data

- Raw facts or values stored in a database (e.g., numbers, text, dates).
- Example below

  | Name  | Age | City        |
  | ----- | --- | ----------- |
  | Alice | 30  | New York    |
  | Bob   | 25  | Los Angeles |

## Table

- A collection of rows and columns that stores data about a specific subject, like Customers or Orders.

## Column (Field)

- A named attribute or data category within a table (e.g., Name, Age).

## Row (Record)

- A single entry or instance in a table, representing a single item or entity.

## Database

A database is an organized collection of data that is stored and accessed electronically. Below are the types of database

## SQL (Structured Query Language)

- The standard language for managing and manipulating relational databases using commands like `SELECT`, `INSERT`, `UPDATE`, and `DELETE`.

## T-SQL (Transact-SQL)

- Microsoft's extension to SQL that adds procedural logic (e.g., `IF`, `WHILE`, error handling) and system-level functions.

## Database Management Systems

![Database Management Systems](./images/DatabaseManagementSystems.jpg "Database Management Systems")

## Relational Database (RDBMS)

- A database that organizes data into tables which are related to each other via keys.

### Relational Database Example: Online Store

Imagine a database for an online store with four related tables:

#### 1. Customers Table

| CustomerID | Name  | Email                                     |
| ---------- | ----- | ----------------------------------------- |
| 1          | Alice | [alice@email.com](mailto:alice@email.com) |
| 2          | Bob   | [bob@email.com](mailto:bob@email.com)     |

- Primary Key: `CustomerID`

#### 2. Orders Table

| OrderID | CustomerID | OrderDate  |
| ------- | ---------- | ---------- |
| 101     | 1          | 2024-06-10 |
| 102     | 2          | 2024-06-11 |
| 103     | 1          | 2024-06-12 |

- Primary Key: `OrderID`
- Foreign Key: `CustomerID` → links to Customers.CustomerID

#### 3. Products Table

| ProductID | ProductName | Price   |
| --------- | ----------- | ------- |
| P1        | Laptop      | 1000.00 |
| P2        | Phone       | 500.00  |

- Primary Key: `ProductID`

#### 4. OrderDetails Table (to link Orders to Products)

| OrderID | ProductID | Quantity |
| ------- | --------- | -------- |
| 101     | P1        | 1        |
| 101     | P2        | 2        |
| 102     | P2        | 1        |

- Composite Primary Key: (`OrderID`, `ProductID`)
- Foreign Keys:

  - `OrderID` → Orders
  - `ProductID` → Products

#### How It's "Relational"

- `Orders` is related to `Customers` via `CustomerID`
- `OrderDetails` is related to `Orders` and `Products`
- You can JOIN these tables in SQL to answer questions like:

  > “What products did Alice order on June 10?”

![Entity Relationship Diagram for the online store](./images/erd.png "Entity Relationship Diagram (ERD) for the online store")

## Relational Database (RDBMS) Solutions

### Microsoft SQL Server

A robust RDBMS by Microsoft, offering enterprise-grade features, scalability, and integration with Windows ecosystems. Widely used in business applications and data analytics.

- [Official Site](https://www.microsoft.com/en-us/sql-server)
- [Download SSMS](https://learn.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms)

### MySQL

An open-source RDBMS known for its speed, reliability, and ease of use. Powers many web applications, including WordPress, and is a popular choice for startups.

- [Official Site](https://www.mysql.com/)
- [Documentation](https://dev.mysql.com/doc/)

### Oracle DB

A high-performance, scalable RDBMS designed for large enterprises. Offers advanced features like partitioning, Real Application Clusters (RAC), and strong security controls.

- [Official Site](https://www.oracle.com/database/)
- [Documentation](https://docs.oracle.com/en/database/)

### PostgreSQL

An advanced open-source RDBMS with support for JSON, geospatial data, and custom extensions. Known for its standards compliance and extensibility.

- [Official Site](https://www.postgresql.org/)
- [Documentation](https://www.postgresql.org/docs/)

## NoSQL Database Solutions

NoSQL databases provide flexible schemas, horizontal scalability, and optimized performance for unstructured or semi-structured data.

### Document: MongoDB

A document-oriented NoSQL database storing data in JSON-like formats. Ideal for agile development, real-time analytics, and handling dynamic schemas.

- [Official Site](https://www.mongodb.com/)
- [MongoDB Atlas](https://www.mongodb.com/atlas/database)

### Key-Value: Redis

An in-memory key-value store with sub-millisecond latency. Used for caching, session management, and real-time applications like leaderboards.

- [Official Site](https://redis.io/)
- [Documentation](https://redis.io/docs/)

### Wide-Column: Apache Cassandra

A distributed NoSQL database designed for high availability and linear scalability. Suited for time-series data, IoT, and applications requiring fault tolerance.

- [Official Site](https://cassandra.apache.org/)
- [Documentation](https://cassandra.apache.org/doc/latest/)

### Graph: Neo4j

A graph database optimized for managing highly connected data. Used in fraud detection, recommendation engines, and social network analysis.

- [Official Site](https://neo4j.com/)
- [Documentation](https://neo4j.com/docs/)

## Other Database Models

### Hierarchical Database

Organizes data in a tree-like structure, best suited for systems with parent-child relationships (e.g., file systems, IBM IMS).

- [Wikipedia](https://en.wikipedia.org/wiki/Hierarchical_database_model)
- [IBM IMS](https://www.ibm.com/products/information-management-system)

### Network Database

Extends hierarchical models with many-to-many relationships, following the CODASYL standard. Rarely used today but foundational in early database systems.

- [Wikipedia](https://en.wikipedia.org/wiki/Network_model)
- [CODASYL Model](https://en.wikipedia.org/wiki/CODASYL)

### Object-Oriented Database

Stores data as objects, supporting inheritance and polymorphism. Used in complex domains like CAD/CAM and scientific applications.

- [Wikipedia](https://en.wikipedia.org/wiki/Object-oriented_database)
- [ObjectDB](https://www.objectdb.com/)

## Cloud & Distributed Databases

### Cloud Database

Fully managed database services (e.g., Amazon RDS, Azure SQL) offering scalability, backups, and high availability without infrastructure overhead.

- [Amazon RDS](https://aws.amazon.com/rds/)
- [Google Cloud SQL](https://cloud.google.com/sql)
- [Azure SQL Database](https://azure.microsoft.com/en-us/products/azure-sql/)

### Distributed Database

Spreads data across multiple nodes for fault tolerance and scalability (e.g., Google Spanner, Cassandra). Ensures consistency and availability in global systems.

- [Wikipedia](https://en.wikipedia.org/wiki/Distributed_database)
- [Google Cloud Spanner](https://cloud.google.com/spanner)
- [Apache Cassandra](https://cassandra.apache.org/)

### Time-Series Database

Optimized for timestamped data (e.g., IoT, monitoring). InfluxDB and TimescaleDB enable efficient storage and querying of time-based metrics.

- [InfluxDB](https://www.influxdata.com/)
- [TimescaleDB](https://www.timescale.com/)

## Data Warehouse

Centralized repositories for analytical reporting, integrating data from multiple sources.

### Solutions

- Azure Synapse Analytics: Unified analytics with big data and SQL integration.
  - [Azure Synapse Analytics](https://azure.microsoft.com/en-us/products/synapse-analytics/)
- Amazon Redshift: Cloud-based data warehousing with columnar storage.
  - [Amazon Redshift](https://aws.amazon.com/redshift/)
- Google BigQuery: Serverless, scalable analytics with SQL support.
  - [Google BigQuery](https://cloud.google.com/bigquery)
- Snowflake: Multi-cloud data warehousing with separation of storage and compute.
  - [Snowflake](https://www.snowflake.com/)
