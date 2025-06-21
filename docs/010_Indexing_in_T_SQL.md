# 010. Indexing in T-SQL

## 1. Understanding Indexes in SQL Server

Indexes are database objects that improve query performance by providing faster data retrieval. They work like a book's index, allowing SQL Server to find data without scanning the entire table.

### Key Benefits of Indexes

- Faster data retrieval
- Improved query performance
- Better sorting and grouping operations
- Enhanced join performance

## 2. Types of Indexes in T-SQL

### A. Clustered Index

- Determines the physical order of data in a table
- Only one per table (the table becomes a "clustered table")
- Best for columns frequently used in range queries

```sql
CREATE CLUSTERED INDEX IX_Orders_OrderID ON Orders(OrderID);
```

### B. Non-Clustered Index

- Separate structure from data storage
- Multiple can exist per table (up to 999 in SQL Server)
- Contains index key values + pointer to data

```sql
CREATE NONCLUSTERED INDEX IX_Customers_Email ON Customers(Email);
```

### C. Unique Index

- Ensures index key contains only unique values
- Can be clustered or non-clustered

```sql
CREATE UNIQUE INDEX UQ_Customers_Phone ON Customers(Phone);
```

### D. Filtered Index

- Optimized index for a subset of data
- Reduces index size and maintenance overhead

```sql
CREATE NONCLUSTERED INDEX IX_Active_Products
ON Products(ProductName)
WHERE Discontinued = 0;
```

### E. Columnstore Index

- Specialized for data warehousing/analytics
- Stores data column-wise rather than row-wise
- Excellent for aggregation queries

```sql
CREATE CLUSTERED COLUMNSTORE INDEX CCI_OrderDetails ON OrderDetails;
```

### F. Full-Text Index

- Special index for text-based searches
- Enables advanced search capabilities

```sql
CREATE FULLTEXT CATALOG ProductCatalog AS DEFAULT;
CREATE FULLTEXT INDEX ON Products(ProductDescription)
KEY INDEX PK_Products;
```

### G. Spatial Index

- For geographic data types (geometry, geography)
- Optimizes spatial queries

```sql
CREATE SPATIAL INDEX SIX_Customer_Locations
ON Customers(Location)
USING GEOGRAPHY_AUTO_GRID;
```

## 3. Creating and Managing Indexes

### Basic Index Creation

```sql
-- Simple non-clustered index
CREATE INDEX IX_Orders_CustomerID ON Orders(CustomerID);

-- Composite index (multiple columns)
CREATE INDEX IX_Orders_DateStatus ON Orders(OrderDate, Status);

-- Index with included columns (covering index)
CREATE INDEX IX_Orders_Covering ON Orders(OrderDate)
INCLUDE (CustomerID, TotalAmount);
```

### Index Maintenance

```sql
-- Rebuild index (fully recreates)
ALTER INDEX IX_Orders_CustomerID ON Orders REBUILD;

-- Reorganize index (defragments)
ALTER INDEX IX_Orders_CustomerID ON Orders REORGANIZE;

-- Disable index
ALTER INDEX IX_Orders_CustomerID ON Orders DISABLE;

-- Drop index
DROP INDEX IX_Orders_CustomerID ON Orders;
```

## 4. Performance Optimization with Indexes

### A. Choosing the Right Columns to Index

- High-selectivity columns (columns with many unique values)
- Frequently filtered columns (WHERE clause)
- Join columns (FOREIGN KEYs)
- Columns in ORDER BY, GROUP BY

### B. Covering Indexes

- Include all columns needed by a query
- Eliminates key lookups to the clustered index

```sql
-- Before (requires lookup)
SELECT OrderID, CustomerID, OrderDate, TotalAmount
FROM Orders
WHERE OrderDate BETWEEN '2023-01-01' AND '2023-12-31';

-- Create covering index
CREATE INDEX IX_Orders_Covering ON Orders(OrderDate)
INCLUDE (CustomerID, TotalAmount);
```

### C. Indexing Strategies for Common Patterns

#### 1. Equality Searches

```sql
-- Good candidate for standard index
CREATE INDEX IX_Customers_Email ON Customers(Email);
```

#### 2. Range Queries

```sql
-- Leading column should be the range column
CREATE INDEX IX_Orders_Date ON Orders(OrderDate);
```

#### 3. Sorting Operations

```sql
-- Index columns in the same order as the sort
CREATE INDEX IX_Products_PriceName ON Products(Price, ProductName);
```

#### 4. Join Optimization

```sql
-- Index join columns on both tables
CREATE INDEX IX_Orders_CustomerID ON Orders(CustomerID);
CREATE INDEX IX_Customers_CustomerID ON Customers(CustomerID);
```

### D. Monitoring Index Usage

```sql
-- Find unused indexes
SELECT
    o.name AS TableName,
    i.name AS IndexName,
    i.type_desc AS IndexType,
    s.user_seeks,
    s.user_scans,
    s.user_lookups
FROM sys.indexes i
INNER JOIN sys.objects o ON i.object_id = o.object_id
LEFT JOIN sys.dm_db_index_usage_stats s ON i.object_id = s.object_id
    AND i.index_id = s.index_id
WHERE o.type = 'U'
    AND i.name IS NOT NULL
    AND (s.user_seeks = 0 AND s.user_scans = 0 AND s.user_lookups = 0)
ORDER BY o.name, i.name;
```

### E. Identifying Missing Indexes

```sql
-- Query the missing index DMVs
SELECT
    migs.avg_total_user_cost * (migs.avg_user_impact / 100.0) * (migs.user_seeks + migs.user_scans) AS improvement_measure,
    mid.statement AS table_name,
    mid.equality_columns,
    mid.inequality_columns,
    mid.included_columns
FROM sys.dm_db_missing_index_group_stats migs
INNER JOIN sys.dm_db_missing_index_groups mig ON migs.group_handle = mig.index_group_handle
INNER JOIN sys.dm_db_missing_index_details mid ON mig.index_handle = mid.index_handle
ORDER BY improvement_measure DESC;
```

## 5. Common Indexing Pitfalls to Avoid

1. Over-indexing - Too many indexes slow down DML operations
2. Under-indexing - Critical queries lack proper indexes
3. Wide indexes - Indexes with too many or too wide columns
4. Duplicate indexes - Multiple indexes on same columns in same order
5. Ignoring clustered index - Not having one or choosing poorly
6. Not maintaining indexes - Fragmentation hurts performance
7. Incorrect column order - Leading columns should match query patterns

## 6. Advanced Indexing Techniques

### A. Indexed Views

```sql
-- Create schema-bound view
CREATE VIEW dbo.vw_OrderSummary WITH SCHEMABINDING AS
SELECT
    CustomerID,
    COUNT_BIG(*) AS OrderCount,
    SUM(TotalAmount) AS TotalSpent
FROM dbo.Orders
GROUP BY CustomerID;
GO

-- Create clustered index on view
CREATE UNIQUE CLUSTERED INDEX IX_vw_OrderSummary
ON dbo.vw_OrderSummary(CustomerID);
```

### B. Partitioned Indexes

```sql
-- Create partition function
CREATE PARTITION FUNCTION pf_OrderDateRange (datetime)
AS RANGE RIGHT FOR VALUES
    ('2020-01-01', '2021-01-01', '2022-01-01', '2023-01-01');
GO

-- Create partition scheme
CREATE PARTITION SCHEME ps_OrderDateRange
AS PARTITION pf_OrderDateRange
TO (fg_2019, fg_2020, fg_2021, fg_2022, fg_2023);
GO

-- Create partitioned index
CREATE CLUSTERED INDEX IX_Orders_OrderDate
ON Orders(OrderDate)
ON ps_OrderDateRange(OrderDate);
```

### C. Filtered Indexes for Sparse Data

```sql
-- Only index non-NULL values
CREATE INDEX IX_Orders_DiscountCode ON Orders(DiscountCode)
WHERE DiscountCode IS NOT NULL;
```

## 7. Index Maintenance Best Practices

1. Regularly rebuild/reorganize fragmented indexes

```sql
-- Rebuild if fragmentation > 30%
ALTER INDEX ALL ON Orders REBUILD WITH (ONLINE = ON);

-- Reorganize if fragmentation between 5-30%
ALTER INDEX ALL ON Orders REORGANIZE;
```

2. Update statistics after index changes

```sql
UPDATE STATISTICS Orders WITH FULLSCAN;
```

3. Schedule index maintenance during low-usage periods

4. Consider ONLINE operations for high-availability systems

```sql
CREATE INDEX IX_Orders_CustomerID ON Orders(CustomerID) WITH (ONLINE = ON);
```

5. Monitor index usage and remove unused indexes

## 8. Real-World Indexing Example

```sql
-- Scenario: E-commerce database optimization

-- 1. Clustered index on Orders table (natural key)
CREATE CLUSTERED INDEX PK_Orders ON Orders(OrderID);

-- 2. Non-clustered indexes for common searches
CREATE INDEX IX_Orders_CustomerID ON Orders(CustomerID);
CREATE INDEX IX_Orders_OrderDate ON Orders(OrderDate);

-- 3. Covering index for frequent order listing query
CREATE INDEX IX_Orders_CustomerDateStatus ON Orders(CustomerID, OrderDate)
INCLUDE (Status, TotalAmount);

-- 4. Filtered index for active products
CREATE INDEX IX_Products_Active ON Products(ProductName, Price)
WHERE Discontinued = 0 AND StockQuantity > 0;

-- 5. Index for search operations
CREATE FULLTEXT CATALOG ProductSearch AS DEFAULT;
CREATE FULLTEXT INDEX ON Products(ProductName, Description)
KEY INDEX PK_Products;

-- 6. Columnstore index for analytics
CREATE CLUSTERED COLUMNSTORE INDEX CCI_OrderDetails ON OrderDetails;
```

By implementing these indexing strategies, you can dramatically improve query performance in your T-SQL applications. Remember to:

- Analyze query patterns before creating indexes
- Test index changes in a non-production environment
- Monitor performance after implementation
- Regularly maintain your indexes
