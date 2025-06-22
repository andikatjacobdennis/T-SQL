# 006. T-SQL DML (Data Manipulation Language) Commands

This guide covers all Data Manipulation Language (DML) commands with executable examples for the `OrderDB` database.

> **Note**
> Technically: SELECT is DQL. Practically (in T-SQL contexts): SELECT is often grouped under DML due to its importance in data operations.

## 1. INSERT (Add New Data)

### Basic INSERT

```sql
-- Insert single row with all columns
INSERT INTO Sales.Customers (FirstName, LastName, Email)
VALUES ('John', 'Doe', 'john.doe@example.com');

-- Insert multiple rows
INSERT INTO Sales.Customers (FirstName, LastName, Email)
VALUES
    ('Jane', 'Smith', 'jane.smith@example.com'),
    ('Bob', 'Johnson', 'bob.johnson@example.com');
```

### INSERT with SELECT

```sql
-- Copy data from another table
INSERT INTO Sales.ArchivedCustomers (CustomerID, Name, Email)
SELECT CustomerID, FirstName + ' ' + LastName, Email
FROM Sales.Customers
WHERE RegistrationDate < '2020-01-01';
```

### INSERT with OUTPUT Clause

```sql
-- Capture inserted identity values
INSERT INTO Sales.Orders (CustomerID, OrderDate)
OUTPUT inserted.OrderID, inserted.CustomerID
VALUES (1, GETDATE());
```

## 2. SELECT (Retrieve Data)

### Basic SELECT

```sql
-- Select all columns
SELECT * FROM Sales.Customers;

-- Select specific columns
SELECT FirstName, LastName, Email
FROM Sales.Customers;
```

### Filtering Data

```sql
-- WHERE clause
SELECT * FROM Sales.Orders
WHERE OrderDate > '2023-01-01';

-- LIKE operator
SELECT * FROM Sales.Customers
WHERE Email LIKE '%@gmail.com';

-- BETWEEN
SELECT * FROM Sales.Orders
WHERE TotalAmount BETWEEN 100 AND 500;
```

### Joining Tables

```sql
-- INNER JOIN
SELECT c.FirstName, c.LastName, o.OrderID, o.OrderDate
FROM Sales.Customers c
INNER JOIN Sales.Orders o ON c.CustomerID = o.CustomerID;

-- LEFT JOIN
SELECT c.FirstName, c.LastName, o.OrderID
FROM Sales.Customers c
LEFT JOIN Sales.Orders o ON c.CustomerID = o.CustomerID;
```

### Aggregation

```sql
-- GROUP BY
SELECT CustomerID, COUNT(*) AS OrderCount
FROM Sales.Orders
GROUP BY CustomerID;

-- HAVING
SELECT CustomerID, SUM(TotalAmount) AS TotalSpent
FROM Sales.Orders
GROUP BY CustomerID
HAVING SUM(TotalAmount) > 1000;
```

## 3. UPDATE (Modify Data)

### Basic UPDATE

```sql
-- Update single record
UPDATE Sales.Customers
SET Email = 'new.email@example.com'
WHERE CustomerID = 1;

-- Update multiple columns
UPDATE Sales.Products
SET Price = Price * 1.1,  -- 10% price increase
    LastUpdated = GETDATE()
WHERE Discontinued = 0;
```

### UPDATE with JOIN

```sql
-- Update based on another table
UPDATE o
SET o.Discount = 0.1
FROM Sales.Orders o
INNER JOIN Sales.Customers c ON o.CustomerID = c.CustomerID
WHERE c.RegistrationDate < '2022-01-01';
```

### UPDATE with OUTPUT

```sql
-- Track changes
UPDATE Sales.Products
SET Price = Price * 1.05
OUTPUT
    deleted.ProductID,
    deleted.Price AS OldPrice,
    inserted.Price AS NewPrice
WHERE CategoryID = 5;
```

## 4. DELETE (Remove Data)

### Basic DELETE

```sql
-- Delete specific records
DELETE FROM Sales.Orders
WHERE OrderDate < '2020-01-01';

-- Delete all records (use TRUNCATE instead for large tables)
DELETE FROM Sales.TempOrders;
```

### DELETE with JOIN

```sql
-- Delete based on another table
DELETE o
FROM Sales.Orders o
INNER JOIN Sales.Customers c ON o.CustomerID = c.CustomerID
WHERE c.Email LIKE '%@olddomain.com';
```

### DELETE with OUTPUT

```sql
-- Capture deleted rows
DELETE FROM Sales.InactiveCustomers
OUTPUT deleted.CustomerID, deleted.Email
WHERE LastActivityDate < DATEADD(YEAR, -2, GETDATE());
```

## 5. MERGE (Upsert Operation)

```sql
-- Synchronize two tables
MERGE INTO Sales.Customers AS target
USING Sales.CustomerUpdates AS source
ON target.CustomerID = source.CustomerID
WHEN MATCHED THEN
    UPDATE SET
        target.FirstName = source.FirstName,
        target.LastName = source.LastName,
        target.Email = source.Email
WHEN NOT MATCHED THEN
    INSERT (CustomerID, FirstName, LastName, Email)
    VALUES (source.CustomerID, source.FirstName, source.LastName, source.Email)
WHEN NOT MATCHED BY SOURCE THEN
    DELETE
OUTPUT $action, inserted.*, deleted.*;
```

## 6. Transaction Control

```sql
-- Explicit transaction
BEGIN TRANSACTION;
BEGIN TRY
    UPDATE Sales.Products
    SET StockQuantity = StockQuantity - 10
    WHERE ProductID = 5;

    INSERT INTO Sales.Orders (CustomerID, ProductID, Quantity)
    VALUES (1, 5, 10);

    COMMIT TRANSACTION;
END TRY
BEGIN CATCH
    ROLLBACK TRANSACTION;
    THROW;
END CATCH;
```

## Complete DML Example Workflow

```sql
-- 1. Insert sample data
INSERT INTO Sales.Customers (FirstName, LastName, Email)
VALUES
    ('Sarah', 'Williams', 'sarah@example.com'),
    ('Michael', 'Brown', 'michael@example.com');

-- 2. Place orders
INSERT INTO Sales.Orders (CustomerID, OrderDate, TotalAmount)
SELECT CustomerID, GETDATE(), 199.99
FROM Sales.Customers
WHERE LastName IN ('Williams', 'Brown');

-- 3. Update customer records
UPDATE Sales.Customers
SET Phone = '555-123-4567'
WHERE Email LIKE '%@example.com';

-- 4. Query data
SELECT
    c.FirstName + ' ' + c.LastName AS CustomerName,
    COUNT(o.OrderID) AS OrderCount,
    SUM(o.TotalAmount) AS TotalSpent
FROM Sales.Customers c
LEFT JOIN Sales.Orders o ON c.CustomerID = o.CustomerID
GROUP BY c.FirstName, c.LastName
ORDER BY TotalSpent DESC;

-- 5. Cleanup (with transaction)
BEGIN TRANSACTION;
DELETE FROM Sales.Orders
WHERE OrderDate < '2022-01-01';

DELETE FROM Sales.Customers
WHERE CustomerID NOT IN (SELECT CustomerID FROM Sales.Orders);
COMMIT TRANSACTION;
```

## DML Best Practices

1. Use transactions for multiple related operations
2. Always include WHERE clauses in UPDATE/DELETE
3. Consider TRUNCATE instead of DELETE for full table clears
4. Use OUTPUT clause to track changes
5. Test SELECTs first before UPDATE/DELETE
6. Use MERGE for complex synchronization tasks
