# 007. T-SQL DQL (Data Query Language) Commands

DQL (Data Query Language) focuses exclusively on retrieving data from databases. While technically SELECT is the only DQL command, it has numerous clauses and options that make it extremely powerful.

## 1. Basic SELECT Statements

### Simple Data Retrieval

```sql
-- Select all columns from a table
SELECT * FROM Customers;

-- Select specific columns
SELECT CustomerID, FirstName, LastName FROM Customers;

-- Select with column aliases
SELECT
    CustomerID AS ID,
    FirstName + ' ' + LastName AS FullName,
    Email AS EmailAddress
FROM Customers;
```

### Limiting Results

```sql
-- Top N records
SELECT TOP 10 * FROM Orders ORDER BY OrderDate DESC;

-- Top N percent
SELECT TOP 25 PERCENT * FROM Products ORDER BY Price DESC;

-- With ties (includes duplicates)
SELECT TOP 5 WITH TIES * FROM Products ORDER BY Price;
```

## 2. Filtering Data

### WHERE Clause

```sql
-- Basic comparison
SELECT * FROM Products WHERE Price > 100;

-- Multiple conditions
SELECT * FROM Orders
WHERE OrderDate BETWEEN '2023-01-01' AND '2023-12-31'
AND TotalAmount > 500;

-- NULL checks
SELECT * FROM Customers WHERE Phone IS NULL;
SELECT * FROM Customers WHERE Phone IS NOT NULL;
```

### Pattern Matching

```sql
-- LIKE operator
SELECT * FROM Customers WHERE Email LIKE '%@gmail.com';

-- Wildcards
SELECT * FROM Products
WHERE ProductName LIKE 'Apple%'; -- Starts with Apple
SELECT * FROM Products
WHERE ProductName LIKE '%Pro%';  -- Contains Pro
SELECT * FROM Products
WHERE ProductName LIKE '_[0-9]%'; -- Second character is digit
```

## 3. Sorting Data

```sql
-- Single column sort
SELECT * FROM Products ORDER BY ProductName;

-- Multiple column sort
SELECT * FROM Customers
ORDER BY LastName ASC, FirstName ASC;

-- Sort by expression
SELECT *, (Price * StockQuantity) AS InventoryValue
FROM Products
ORDER BY InventoryValue DESC;
```

## 4. Grouping and Aggregation

### Basic Aggregation

```sql
-- Count all rows
SELECT COUNT(*) AS TotalCustomers FROM Customers;

-- Count distinct values
SELECT COUNT(DISTINCT Country) AS UniqueCountries FROM Customers;

-- Other aggregate functions
SELECT
    MIN(Price) AS MinPrice,
    MAX(Price) AS MaxPrice,
    AVG(Price) AS AvgPrice,
    SUM(StockQuantity) AS TotalInventory
FROM Products;
```

### GROUP BY

```sql
-- Simple grouping
SELECT Country, COUNT(*) AS CustomerCount
FROM Customers
GROUP BY Country;

-- Grouping with multiple columns
SELECT
    YEAR(OrderDate) AS OrderYear,
    MONTH(OrderDate) AS OrderMonth,
    COUNT(*) AS OrderCount
FROM Orders
GROUP BY YEAR(OrderDate), MONTH(OrderDate);
```

### HAVING Clause

```sql
-- Filter groups
SELECT
    CustomerID,
    COUNT(*) AS OrderCount,
    SUM(TotalAmount) AS TotalSpent
FROM Orders
GROUP BY CustomerID
HAVING COUNT(*) > 5 AND SUM(TotalAmount) > 1000;
```

## 5. Joining Tables

### INNER JOIN

```sql
SELECT
    c.CustomerID,
    c.FirstName + ' ' + c.LastName AS CustomerName,
    o.OrderID,
    o.OrderDate,
    o.TotalAmount
FROM Customers c
INNER JOIN Orders o ON c.CustomerID = o.CustomerID;
```

### OUTER JOINS

```sql
-- LEFT JOIN (all customers, even without orders)
SELECT
    c.CustomerID,
    c.FirstName,
    c.LastName,
    o.OrderID
FROM Customers c
LEFT JOIN Orders o ON c.CustomerID = o.CustomerID;

-- RIGHT JOIN (all orders, even without customer info)
SELECT
    o.OrderID,
    c.FirstName,
    c.LastName
FROM Orders o
RIGHT JOIN Customers c ON o.CustomerID = c.CustomerID;

-- FULL JOIN (all records from both tables)
SELECT
    c.CustomerID,
    o.OrderID
FROM Customers c
FULL JOIN Orders o ON c.CustomerID = o.CustomerID;
```

### CROSS JOIN

```sql
-- Cartesian product
SELECT
    p.ProductName,
    c.CategoryName
FROM Products p
CROSS JOIN Categories c;
```

## 6. Subqueries

### WHERE Clause Subqueries

```sql
-- Single value subquery
SELECT * FROM Products
WHERE Price > (SELECT AVG(Price) FROM Products);

-- IN subquery
SELECT * FROM Customers
WHERE CustomerID IN (
    SELECT DISTINCT CustomerID FROM Orders
    WHERE OrderDate > '2023-01-01'
);

-- EXISTS subquery
SELECT * FROM Customers c
WHERE EXISTS (
    SELECT 1 FROM Orders o
    WHERE o.CustomerID = c.CustomerID
    AND o.TotalAmount > 1000
);
```

### FROM Clause Subqueries

```sql
SELECT
    OrderYear,
    COUNT(*) AS OrderCount
FROM (
    SELECT
        YEAR(OrderDate) AS OrderYear,
        CustomerID
    FROM Orders
) AS OrderSummary
GROUP BY OrderYear;
```

### SELECT Clause Subqueries

```sql
SELECT
    CustomerID,
    FirstName,
    LastName,
    (SELECT COUNT(*) FROM Orders o
     WHERE o.CustomerID = c.CustomerID) AS OrderCount
FROM Customers c;
```

## 7. Common Table Expressions (CTEs)

### Basic CTE

```sql
WITH HighValueOrders AS (
    SELECT * FROM Orders
    WHERE TotalAmount > 1000
)
SELECT
    c.FirstName,
    c.LastName,
    h.OrderID,
    h.TotalAmount
FROM Customers c
JOIN HighValueOrders h ON c.CustomerID = h.CustomerID;
```

### Recursive CTE

```sql
WITH EmployeeHierarchy AS (
    -- Anchor member
    SELECT
        EmployeeID,
        FirstName,
        LastName,
        ManagerID,
        1 AS Level
    FROM Employees
    WHERE ManagerID IS NULL

    UNION ALL

    -- Recursive member
    SELECT
        e.EmployeeID,
        e.FirstName,
        e.LastName,
        e.ManagerID,
        eh.Level + 1
    FROM Employees e
    JOIN EmployeeHierarchy eh ON e.ManagerID = eh.EmployeeID
)
SELECT * FROM EmployeeHierarchy
ORDER BY Level, LastName;
```

## 8. Window Functions

### Ranking Functions

```sql
-- ROW_NUMBER
SELECT
    ProductID,
    ProductName,
    Price,
    ROW_NUMBER() OVER (ORDER BY Price DESC) AS PriceRank
FROM Products;

-- RANK (with ties)
SELECT
    ProductID,
    ProductName,
    Price,
    RANK() OVER (ORDER BY Price DESC) AS PriceRank
FROM Products;

-- DENSE_RANK
SELECT
    DepartmentID,
    EmployeeName,
    Salary,
    DENSE_RANK() OVER (PARTITION BY DepartmentID ORDER BY Salary DESC) AS DeptSalaryRank
FROM Employees;
```

### Analytic Functions

```sql
-- Running total
SELECT
    OrderID,
    OrderDate,
    TotalAmount,
    SUM(TotalAmount) OVER (ORDER BY OrderDate) AS RunningTotal
FROM Orders;

-- Moving average
SELECT
    OrderDate,
    TotalAmount,
    AVG(TotalAmount) OVER (
        ORDER BY OrderDate
        ROWS BETWEEN 2 PRECEDING AND CURRENT ROW
    ) AS ThreeDayMovingAvg
FROM Orders;
```

## 9. Pivoting and Unpivoting

### PIVOT

```sql
SELECT *
FROM (
    SELECT
        YEAR(OrderDate) AS OrderYear,
        MONTH(OrderDate) AS OrderMonth,
        TotalAmount
    FROM Orders
) AS SourceData
PIVOT (
    SUM(TotalAmount)
    FOR OrderMonth IN ([1], [2], [3], [4], [5], [6], [7], [8], [9], [10], [11], [12])
) AS PivotTable;
```

### UNPIVOT

```sql
SELECT ProductID, Quarter, Sales
FROM (
    SELECT
        ProductID,
        Q1_Sales,
        Q2_Sales,
        Q3_Sales,
        Q4_Sales
    FROM ProductSales
) AS SourceData
UNPIVOT (
    Sales FOR Quarter IN (Q1_Sales, Q2_Sales, Q3_Sales, Q4_Sales)
) AS UnpivotTable;
```

## 10. Full-Text Search

```sql
-- Search for products containing words
SELECT * FROM Products
WHERE CONTAINS(ProductDescription, '"computer" NEAR "monitor"');

-- Search with wildcards
SELECT * FROM Products
WHERE FREETEXT(ProductDescription, 'fast reliable laptop');

-- Weighted search
SELECT * FROM Products
WHERE CONTAINS(
    (ProductName, ProductDescription),
    'ISABOUT("computer" WEIGHT(0.8), "accessory" WEIGHT(0.2))'
);
```

## 11. JSON and XML Queries

### JSON Functions

```sql
-- Extract JSON values
SELECT
    OrderID,
    JSON_VALUE(OrderDetails, '$.Customer.Name') AS CustomerName,
    JSON_VALUE(OrderDetails, '$.OrderDate') AS OrderDate
FROM OrdersWithJSON;

-- Query JSON array
SELECT
    OrderID,
    p.ProductName,
    p.Quantity
FROM OrdersWithJSON
CROSS APPLY OPENJSON(OrderDetails, '$.Products') WITH (
    ProductName NVARCHAR(100) '$.Name',
    Quantity INT '$.Qty'
) AS p;
```

### XML Functions

```sql
-- Query XML data
SELECT
    OrderID,
    OrderXML.value('(/Order/Customer/Name)[1]', 'NVARCHAR(100)') AS CustomerName,
    OrderXML.value('(/Order/Date)[1]', 'DATETIME') AS OrderDate
FROM OrdersWithXML;

-- Shred XML to rows
SELECT
    o.OrderID,
    p.ProductName,
    p.Quantity
FROM OrdersWithXML o
CROSS APPLY OrderXML.nodes('/Order/Products/Product') AS t(c)
CROSS APPLY (SELECT
    c.value('(Name)[1]', 'NVARCHAR(100)') AS ProductName,
    c.value('(Quantity)[1]', 'INT') AS Quantity
) AS p;
```

## 12. Query Performance Techniques

### Execution Plan Hints

```sql
-- Force index usage
SELECT * FROM Customers WITH (INDEX(IX_Customers_Email))
WHERE Email LIKE '%@gmail.com';

-- Force join type
SELECT * FROM Customers c
INNER LOOP JOIN Orders o ON c.CustomerID = o.CustomerID;

-- Optimize for specific parameter
SELECT * FROM Orders
WHERE OrderDate > @StartDate
OPTION (OPTIMIZE FOR (@StartDate = '2023-01-01'));
```

### Query Store Hints

```sql
-- Force a specific plan
EXEC sp_query_store_force_plan @query_id = 123, @plan_id = 456;

-- Add query hint
SELECT * FROM LargeTable
OPTION (MAXDOP 4, USE HINT('ENABLE_PARALLEL_PLAN_PREFERENCE'));
```

## 13. User-Created Databases

```sql
SELECT name
FROM sys.databases
WHERE database_id > 4  -- Excludes system databases (master, tempdb, model, msdb)
ORDER BY name;
```

## 14. User-Created Stored Procedures

```sql
-- In current database
SELECT name, create_date
FROM sys.procedures
WHERE is_ms_shipped = 0  -- Excludes system objects
ORDER BY name;
```

## 15. User-Created Functions

```sql
SELECT
    o.name,
    CASE o.type
        WHEN 'FN' THEN 'Scalar function'
        WHEN 'IF' THEN 'Inline table function'
        WHEN 'TF' THEN 'Table-valued function'
    END AS function_type,
    o.create_date
FROM sys.objects o
WHERE o.type IN ('FN', 'IF', 'TF')
AND o.is_ms_shipped = 0
ORDER BY o.name;
```

## 16. User-Created Triggers

```sql
-- DML triggers
SELECT name, parent_id, create_date
FROM sys.triggers
WHERE is_ms_shipped = 0
ORDER BY name;

-- DDL triggers
SELECT name, create_date
FROM sys.server_triggers
WHERE is_ms_shipped = 0
ORDER BY name;
```

## 17. User-Created Views

```sql
SELECT name, create_date
FROM sys.views
WHERE is_ms_shipped = 0
ORDER BY name;
```

## 18. All User-Created Objects Together

```sql
SELECT
    SCHEMA_NAME(schema_id) AS schema_name,
    name AS object_name,
    type_desc,
    create_date
FROM sys.objects
WHERE is_ms_shipped = 0
AND type IN ('P','FN','IF','TF','TR','V','U')  -- P=Proc, FN=Func, etc.
ORDER BY type_desc, schema_name, object_name;
```

## 19. User-Created Tables

```sql
SELECT
    SCHEMA_NAME(schema_id) AS schema_name,
    name AS table_name,
    create_date
FROM sys.tables
WHERE is_ms_shipped = 0
ORDER BY schema_name, table_name;
```
