# 012. Frequently Asked Questions

## Basic Level Questions (1-30)

### 1. What is T-SQL?
**Answer:**
T-SQL (Transact-SQL) is Microsoft's extension of SQL used in SQL Server. It adds programming features like variables, loops, conditionals, error handling, and stored procedures to standard SQL. 

### 2. How do you retrieve all columns from a table?
**Answer:**
```sql
-- Using SELECT * (though it's better practice to specify columns)
SELECT * FROM Employees;
```

### 3. How do you retrieve specific columns from a table?
**Answer:**
```sql
SELECT EmployeeID, FirstName, LastName FROM Employees;
```

### 4. How do you filter rows in a SELECT statement?
**Answer:**
```sql
SELECT * FROM Employees WHERE Department = 'IT';
```

### 5. How do you sort results in a SELECT statement?
**Answer:**
```sql
SELECT * FROM Employees ORDER BY LastName ASC, FirstName ASC;
```

### 6. How do you create a new table?
**Answer:**
```sql
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    FirstName NVARCHAR(50),
    LastName NVARCHAR(50),
    HireDate DATE,
    Salary DECIMAL(10,2)
);
```

### 7. How do you insert data into a table?
**Answer:**
```sql
INSERT INTO Employees (EmployeeID, FirstName, LastName, HireDate, Salary)
VALUES (1, 'John', 'Doe', '2020-01-15', 75000.00);
```

### 8. How do you update existing data in a table?
**Answer:**
```sql
UPDATE Employees 
SET Salary = 80000.00 
WHERE EmployeeID = 1;
```

### 9. How do you delete data from a table?
**Answer:**
```sql
DELETE FROM Employees WHERE EmployeeID = 1;
```

### 10. What are the different types of joins in T-SQL?
**Answer:**
```sql
-- INNER JOIN: Returns rows when there's a match in both tables
SELECT e.FirstName, d.DepartmentName 
FROM Employees e
INNER JOIN Departments d ON e.DepartmentID = d.DepartmentID;

-- LEFT JOIN: Returns all rows from left table, matched rows from right
SELECT e.FirstName, d.DepartmentName 
FROM Employees e
LEFT JOIN Departments d ON e.DepartmentID = d.DepartmentID;

-- RIGHT JOIN: Returns all rows from right table, matched rows from left
SELECT e.FirstName, d.DepartmentName 
FROM Employees e
RIGHT JOIN Departments d ON e.DepartmentID = d.DepartmentID;

-- FULL JOIN: Returns rows when there's a match in either table
SELECT e.FirstName, d.DepartmentName 
FROM Employees e
FULL JOIN Departments d ON e.DepartmentID = d.DepartmentID;
```

### 11. How do you use GROUP BY?
**Answer:**
```sql
SELECT DepartmentID, COUNT(*) AS EmployeeCount
FROM Employees
GROUP BY DepartmentID;
```

### 12. How do you use HAVING clause?
**Answer:**
```sql
SELECT DepartmentID, COUNT(*) AS EmployeeCount
FROM Employees
GROUP BY DepartmentID
HAVING COUNT(*) > 5;
```

### 13. What is the difference between WHERE and HAVING?
**Answer:**
```sql
-- WHERE filters rows before grouping
SELECT DepartmentID, COUNT(*) AS EmployeeCount
FROM Employees
WHERE Salary > 50000
GROUP BY DepartmentID;

-- HAVING filters groups after grouping
SELECT DepartmentID, COUNT(*) AS EmployeeCount
FROM Employees
GROUP BY DepartmentID
HAVING COUNT(*) > 5;
```

### 14. How do you use DISTINCT?
**Answer:**
```sql
SELECT DISTINCT Department FROM Employees;
```

### 15. What are aggregate functions in T-SQL?
**Answer:**
```sql
SELECT 
    COUNT(*) AS TotalEmployees,
    AVG(Salary) AS AverageSalary,
    SUM(Salary) AS TotalSalary,
    MIN(Salary) AS MinimumSalary,
    MAX(Salary) AS MaximumSalary
FROM Employees;
```

### 16. How do you use BETWEEN?
**Answer:**
```sql
SELECT * FROM Employees 
WHERE Salary BETWEEN 40000 AND 80000;
```

### 17. How do you use IN operator?
**Answer:**
```sql
SELECT * FROM Employees 
WHERE Department IN ('IT', 'Finance', 'HR');
```

### 18. How do you use LIKE operator?
**Answer:**
```sql
-- % for any string of zero or more characters
SELECT * FROM Employees WHERE LastName LIKE 'Sm%';

-- _ for any single character
SELECT * FROM Employees WHERE LastName LIKE 'Sm_th';

-- [] for any single character within the range/set
SELECT * FROM Employees WHERE LastName LIKE 'Sm[a-i]th';
```

### 19. How do you create a view?
**Answer:**
```sql
CREATE VIEW ITEmployees AS
SELECT EmployeeID, FirstName, LastName
FROM Employees
WHERE Department = 'IT';
```

### 20. How do you use IS NULL and IS NOT NULL?
**Answer:**
```sql
SELECT * FROM Employees WHERE ManagerID IS NULL;
SELECT * FROM Employees WHERE ManagerID IS NOT NULL;
```

### 21. What are the different data types in SQL Server?
**Answer:**
```sql
-- Common data types:
-- Exact numerics: INT, BIGINT, SMALLINT, TINYINT, DECIMAL, NUMERIC
-- Approximate numerics: FLOAT, REAL
-- Date and time: DATE, TIME, DATETIME, DATETIME2, SMALLDATETIME
-- Character strings: CHAR, VARCHAR, TEXT
-- Unicode strings: NCHAR, NVARCHAR, NTEXT
-- Binary: BINARY, VARBINARY, IMAGE
-- Other: BIT, UNIQUEIDENTIFIER, XML, TABLE
```

### 22. How do you add a column to an existing table?
**Answer:**
```sql
ALTER TABLE Employees
ADD Email NVARCHAR(100);
```

### 23. How do you modify a column in an existing table?
**Answer:**
```sql
ALTER TABLE Employees
ALTER COLUMN Email NVARCHAR(150);
```

### 24. How do you drop a column from a table?
**Answer:**
```sql
ALTER TABLE Employees
DROP COLUMN Email;
```

### 25. How do you rename a table?
**Answer:**
```sql
EXEC sp_rename 'OldTableName', 'NewTableName';
```

### 26. How do you rename a column?
**Answer:**
```sql
EXEC sp_rename 'Employees.Email', 'EmailAddress', 'COLUMN';
```

### 27. What is a primary key?
**Answer:**
```sql
-- A primary key uniquely identifies each row in a table
-- It cannot contain NULL values and must contain unique values
CREATE TABLE Products (
    ProductID INT PRIMARY KEY,
    ProductName NVARCHAR(100) NOT NULL
);
```

### 28. What is a foreign key?
**Answer:**
```sql
-- A foreign key is a field that refers to the primary key in another table
CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    ProductID INT FOREIGN KEY REFERENCES Products(ProductID),
    OrderDate DATE
);
```

### 29. How do you create a composite primary key?
**Answer:**
```sql
CREATE TABLE OrderDetails (
    OrderID INT,
    ProductID INT,
    Quantity INT,
    PRIMARY KEY (OrderID, ProductID)
);
```

### 30. What is the difference between DELETE, TRUNCATE, and DROP?
**Answer:**
```sql
-- DELETE removes rows one at a time, logs each row, can use WHERE, can be rolled back
DELETE FROM Employees WHERE EmployeeID = 1;

-- TRUNCATE removes all rows at once, minimal logging, faster, can't use WHERE, can't be rolled back
TRUNCATE TABLE TempEmployees;

-- DROP removes the entire table structure including data
DROP TABLE OldEmployees;
```

## Intermediate Level Questions (31-70)

### 31. What are stored procedures?
**Answer:**
```sql
CREATE PROCEDURE GetEmployeeByID
    @EmployeeID INT
AS
BEGIN
    SELECT * FROM Employees WHERE EmployeeID = @EmployeeID;
END;
GO

-- Execute the stored procedure
EXEC GetEmployeeByID @EmployeeID = 1;
```

### 32. What are functions in T-SQL?
**Answer:**
```sql
-- Scalar function
CREATE FUNCTION GetFullName(@FirstName NVARCHAR(50), @LastName NVARCHAR(50))
RETURNS NVARCHAR(101)
AS
BEGIN
    RETURN @FirstName + ' ' + @LastName;
END;
GO

-- Table-valued function
CREATE FUNCTION GetEmployeesByDepartment(@DeptName NVARCHAR(50))
RETURNS TABLE
AS
RETURN
    SELECT * FROM Employees WHERE Department = @DeptName;
GO

-- Usage
SELECT dbo.GetFullName(FirstName, LastName) AS FullName FROM Employees;
SELECT * FROM dbo.GetEmployeesByDepartment('IT');
```

### 33. What are table variables?
**Answer:**
```sql
DECLARE @EmployeeTable TABLE (
    EmployeeID INT,
    FullName NVARCHAR(101),
    Department NVARCHAR(50)
);

INSERT INTO @EmployeeTable
SELECT EmployeeID, FirstName + ' ' + LastName, Department
FROM Employees;

SELECT * FROM @EmployeeTable;
```

### 34. What are temporary tables?
**Answer:**
```sql
-- Local temporary table (visible only to current session)
CREATE TABLE #TempEmployees (
    EmployeeID INT,
    FullName NVARCHAR(101)
);

-- Global temporary table (visible to all sessions)
CREATE TABLE ##GlobalTempEmployees (
    EmployeeID INT,
    FullName NVARCHAR(101)
);

-- Insert data
INSERT INTO #TempEmployees
SELECT EmployeeID, FirstName + ' ' + LastName
FROM Employees;

-- Query
SELECT * FROM #TempEmployees;

-- Drop when done
DROP TABLE #TempEmployees;
```

### 35. What are common table expressions (CTEs)?
**Answer:**
```sql
WITH DepartmentStats AS (
    SELECT 
        Department,
        COUNT(*) AS EmployeeCount,
        AVG(Salary) AS AvgSalary
    FROM Employees
    GROUP BY Department
)
SELECT * FROM DepartmentStats
WHERE EmployeeCount > 5
ORDER BY AvgSalary DESC;
```

### 36. What is a recursive CTE?
**Answer:**
```sql
-- Example: Employee hierarchy
WITH EmployeeHierarchy AS (
    -- Anchor member
    SELECT 
        EmployeeID,
        FirstName,
        LastName,
        ManagerID,
        0 AS Level
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
    INNER JOIN EmployeeHierarchy eh ON e.ManagerID = eh.EmployeeID
)
SELECT * FROM EmployeeHierarchy
ORDER BY Level, LastName, FirstName;
```

### 37. What are window functions?
**Answer:**
```sql
SELECT 
    EmployeeID,
    FirstName,
    LastName,
    Department,
    Salary,
    RANK() OVER (PARTITION BY Department ORDER BY Salary DESC) AS DeptSalaryRank,
    DENSE_RANK() OVER (PARTITION BY Department ORDER BY Salary DESC) AS DeptSalaryDenseRank,
    ROW_NUMBER() OVER (PARTITION BY Department ORDER BY Salary DESC) AS DeptSalaryRowNum,
    NTILE(4) OVER (ORDER BY Salary DESC) AS SalaryQuartile,
    LAG(Salary, 1) OVER (PARTITION BY Department ORDER BY Salary) AS PrevSalary,
    LEAD(Salary, 1) OVER (PARTITION BY Department ORDER BY Salary) AS NextSalary,
    FIRST_VALUE(Salary) OVER (PARTITION BY Department ORDER BY Salary) AS DeptMinSalary,
    LAST_VALUE(Salary) OVER (PARTITION BY Department ORDER BY Salary) AS DeptMaxSalary
FROM Employees;
```

### 38. How do you use PIVOT?
**Answer:**
```sql
-- Pivot example: Department vs. Salary totals
SELECT Department, [2019], [2020], [2021]
FROM (
    SELECT 
        Department, 
        YEAR(HireDate) AS HireYear,
        Salary
    FROM Employees
) AS SourceTable
PIVOT (
    SUM(Salary)
    FOR HireYear IN ([2019], [2020], [2021])
) AS PivotTable;
```

### 39. How do you use UNPIVOT?
**Answer:**
```sql
-- First create a sample pivoted table
SELECT Department, [2019], [2020], [2021] 
INTO #PivotedData
FROM (
    SELECT Department, YEAR(HireDate) AS HireYear, COUNT(*) AS EmployeeCount
    FROM Employees
    GROUP BY Department, YEAR(HireDate)
) AS SourceTable
PIVOT (
    SUM(EmployeeCount)
    FOR HireYear IN ([2019], [2020], [2021])
) AS PivotTable;

-- Now unpivot it
SELECT Department, Year, EmployeeCount
FROM #PivotedData
UNPIVOT (
    EmployeeCount FOR Year IN ([2019], [2020], [2021])
) AS UnpivotTable;
```

### 40. What are transactions in T-SQL?
**Answer:**
```sql
BEGIN TRY
    BEGIN TRANSACTION;
    
    -- Transfer $100 from account 1 to account 2
    UPDATE Accounts SET Balance = Balance - 100 WHERE AccountID = 1;
    UPDATE Accounts SET Balance = Balance + 100 WHERE AccountID = 2;
    
    COMMIT TRANSACTION;
END TRY
BEGIN CATCH
    IF @@TRANCOUNT > 0
        ROLLBACK TRANSACTION;
    
    THROW;
END CATCH
```

### 41. What are the different isolation levels?
**Answer:**
```sql
-- Read Uncommitted (dirty reads allowed)
SET TRANSACTION ISOLATION LEVEL READ UNCOMMITTED;

-- Read Committed (default, prevents dirty reads)
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;

-- Repeatable Read (locks prevent changes to data read by transaction)
SET TRANSACTION ISOLATION LEVEL REPEATABLE READ;

-- Serializable (highest isolation, prevents phantom reads)
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;

-- Snapshot (uses row versioning instead of locks)
SET TRANSACTION ISOLATION LEVEL SNAPSHOT;
```

### 42. What are the different types of locks?
**Answer:**
```sql
-- Common lock types:
-- Shared (S) - For read operations
-- Exclusive (X) - For write operations
-- Update (U) - For update operations
-- Intent (IS, IX, IU) - Indicates intention to place locks at lower level
-- Schema (Sch-M, Sch-S) - For schema modifications
-- Bulk Update (BU) - For bulk operations
```

### 43. How do you handle errors in T-SQL?
**Answer:**
```sql
BEGIN TRY
    -- Code that might cause an error
    SELECT 1/0;
END TRY
BEGIN CATCH
    SELECT 
        ERROR_NUMBER() AS ErrorNumber,
        ERROR_SEVERITY() AS ErrorSeverity,
        ERROR_STATE() AS ErrorState,
        ERROR_PROCEDURE() AS ErrorProcedure,
        ERROR_LINE() AS ErrorLine,
        ERROR_MESSAGE() AS ErrorMessage;
END CATCH
```

### 44. What is the difference between UNION and UNION ALL?
**Answer:**
```sql
-- UNION removes duplicates and sorts results
SELECT FirstName FROM Employees WHERE Department = 'IT'
UNION
SELECT FirstName FROM Employees WHERE Department = 'HR';

-- UNION ALL includes all rows including duplicates
SELECT FirstName FROM Employees WHERE Department = 'IT'
UNION ALL
SELECT FirstName FROM Employees WHERE Department = 'HR';
```

### 45. What is the difference between INNER JOIN and OUTER JOIN?
**Answer:**
```sql
-- INNER JOIN returns only matching rows
SELECT e.FirstName, d.DepartmentName
FROM Employees e
INNER JOIN Departments d ON e.DepartmentID = d.DepartmentID;

-- OUTER JOIN (LEFT, RIGHT, FULL) returns all rows from one/both tables
-- with NULLs for non-matching rows
SELECT e.FirstName, d.DepartmentName
FROM Employees e
LEFT JOIN Departments d ON e.DepartmentID = d.DepartmentID;
```

### 46. What is a self-join?
**Answer:**
```sql
-- Joining a table to itself (e.g., employee-manager relationship)
SELECT 
    e.FirstName + ' ' + e.LastName AS Employee,
    m.FirstName + ' ' + m.LastName AS Manager
FROM Employees e
LEFT JOIN Employees m ON e.ManagerID = m.EmployeeID;
```

### 47. What is a cross join?
**Answer:**
```sql
-- Cartesian product of all rows from both tables
SELECT e.FirstName, d.DepartmentName
FROM Employees e
CROSS JOIN Departments d;
```

### 48. How do you use EXISTS?
**Answer:**
```sql
-- Find employees who have at least one order
SELECT e.FirstName, e.LastName
FROM Employees e
WHERE EXISTS (
    SELECT 1 FROM Orders o 
    WHERE o.EmployeeID = e.EmployeeID
);
```

### 49. How do you use NOT EXISTS?
**Answer:**
```sql
-- Find employees with no orders
SELECT e.FirstName, e.LastName
FROM Employees e
WHERE NOT EXISTS (
    SELECT 1 FROM Orders o 
    WHERE o.EmployeeID = e.EmployeeID
);
```

### 50. What is the difference between EXISTS and IN?
**Answer:**
```sql
-- EXISTS is often more efficient with correlated subqueries
SELECT e.FirstName, e.LastName
FROM Employees e
WHERE EXISTS (
    SELECT 1 FROM Orders o 
    WHERE o.EmployeeID = e.EmployeeID
);

-- IN is better with static lists or non-correlated subqueries
SELECT e.FirstName, e.LastName
FROM Employees e
WHERE e.EmployeeID IN (
    SELECT DISTINCT EmployeeID FROM Orders
);
```

### 51. What is the difference between IN and = ANY?
**Answer:**
```sql
-- IN and = ANY are functionally equivalent
SELECT * FROM Employees 
WHERE Department IN ('IT', 'HR', 'Finance');

SELECT * FROM Employees 
WHERE Department = ANY (SELECT Department FROM Departments WHERE Active = 1);
```

### 52. What is the difference between NOT IN and <> ALL?
**Answer:**
```sql
-- NOT IN and <> ALL are functionally equivalent
SELECT * FROM Employees 
WHERE Department NOT IN ('IT', 'HR', 'Finance');

SELECT * FROM Employees 
WHERE Department <> ALL (SELECT Department FROM Departments WHERE Active = 0);
```

### 53. How do you use CASE expressions?
**Answer:**
```sql
SELECT 
    EmployeeID,
    FirstName,
    LastName,
    Salary,
    CASE 
        WHEN Salary < 50000 THEN 'Low'
        WHEN Salary BETWEEN 50000 AND 100000 THEN 'Medium'
        ELSE 'High'
    END AS SalaryRange,
    CASE Department
        WHEN 'IT' THEN 'Technology'
        WHEN 'HR' THEN 'Human Resources'
        ELSE 'Other'
    END AS DepartmentGroup
FROM Employees;
```

### 54. How do you use COALESCE?
**Answer:**
```sql
-- Returns first non-NULL expression
SELECT 
    EmployeeID,
    COALESCE(MiddleName, '') AS MiddleName,
    COALESCE(ManagerID, 0) AS ManagerID
FROM Employees;
```

### 55. How do you use ISNULL?
**Answer:**
```sql
-- Replaces NULL with specified value (SQL Server specific)
SELECT 
    EmployeeID,
    ISNULL(MiddleName, '') AS MiddleName,
    ISNULL(ManagerID, 0) AS ManagerID
FROM Employees;
```

### 56. What is the difference between COALESCE and ISNULL?
**Answer:**
```sql
-- COALESCE is ANSI standard, can take multiple parameters
SELECT COALESCE(NULL, NULL, 'Third', 'Fourth') AS Result; -- Returns 'Third'

-- ISNULL is SQL Server specific, takes exactly 2 parameters
SELECT ISNULL(NULL, 'Default') AS Result; -- Returns 'Default'

-- Data type differences:
-- ISNULL uses data type of first parameter
-- COALESCE uses data type with highest precedence
```

### 57. How do you use NULLIF?
**Answer:**
```sql
-- Returns NULL if the two expressions are equal
SELECT 
    EmployeeID,
    NULLIF(TerminationDate, '9999-12-31') AS ActualTerminationDate
FROM Employees;
```

### 58. How do you use IIF?
**Answer:**
```sql
-- Shorthand for simple CASE expression
SELECT 
    EmployeeID,
    IIF(Salary > 100000, 'High Earner', 'Regular') AS EarningsCategory
FROM Employees;
```

### 59. How do you use CHOOSE?
**Answer:**
```sql
-- Returns item at specified index (1-based)
SELECT 
    EmployeeID,
    CHOOSE(MONTH(HireDate), 'Winter', 'Winter', 'Spring', 'Spring', 'Spring', 
           'Summer', 'Summer', 'Summer', 'Fall', 'Fall', 'Fall', 'Winter') AS HiringSeason
FROM Employees;
```

### 60. How do you use TRY_CAST and TRY_CONVERT?
**Answer:**
```sql
-- TRY_CAST returns NULL instead of error if conversion fails
SELECT TRY_CAST('ABC' AS INT) AS Result; -- Returns NULL

-- TRY_CONVERT is similar but SQL Server specific with style parameter
SELECT TRY_CONVERT(DATETIME, '2023-02-30', 101) AS Result; -- Returns NULL
```

### 61. How do you use STRING_AGG?
**Answer:**
```sql
-- Concatenates values with a separator
SELECT 
    Department,
    STRING_AGG(FirstName + ' ' + LastName, ', ') AS Employees
FROM Employees
GROUP BY Department;
```

### 62. How do you use STRING_SPLIT?
**Answer:**
```sql
-- Splits a string into rows based on a separator
SELECT value AS Item
FROM STRING_SPLIT('apple,orange,banana', ',');
```

### 63. How do you use JSON functions?
**Answer:**
```sql
-- FOR JSON to generate JSON
SELECT EmployeeID, FirstName, LastName
FROM Employees
FOR JSON PATH;

-- JSON_VALUE to extract scalar value
SELECT JSON_VALUE('{"name": "John", "age": 30}', '$.name') AS Name;

-- JSON_QUERY to extract object/array
SELECT JSON_QUERY('{"name": "John", "address": {"city": "NY"}}', '$.address') AS Address;

-- OPENJSON to parse JSON into rows
DECLARE @json NVARCHAR(MAX) = N'[
    {"id": 1, "name": "John"},
    {"id": 2, "name": "Jane"}
]';

SELECT * FROM OPENJSON(@json)
WITH (
    id INT '$.id',
    name NVARCHAR(50) '$.name'
);
```

### 64. How do you use XML functions?
**Answer:**
```sql
-- FOR XML to generate XML
SELECT EmployeeID AS "@id", FirstName, LastName
FROM Employees
FOR XML PATH('Employee'), ROOT('Employees');

-- XQuery methods
DECLARE @xml XML = '
<Employees>
    <Employee id="1">
        <FirstName>John</FirstName>
        <LastName>Doe</LastName>
    </Employee>
</Employees>';

SELECT 
    @xml.value('(/Employees/Employee/FirstName)[1]', 'NVARCHAR(50)') AS FirstName,
    @xml.query('/Employees/Employee') AS EmployeeNode;
```

### 65. What are triggers?
**Answer:**
```sql
-- AFTER trigger example
CREATE TRIGGER trg_AfterEmployeeInsert
ON Employees
AFTER INSERT
AS
BEGIN
    INSERT INTO EmployeeAudit(EmployeeID, Action, ActionDate)
    SELECT EmployeeID, 'INSERT', GETDATE()
    FROM inserted;
END;
GO

-- INSTEAD OF trigger example
CREATE TRIGGER trg_InsteadOfDelete
ON Employees
INSTEAD OF DELETE
AS
BEGIN
    UPDATE Employees
    SET Active = 0
    WHERE EmployeeID IN (SELECT EmployeeID FROM deleted);
END;
GO
```

### 66. What are the different types of indexes?
**Answer:**
```sql
-- Clustered index (one per table, determines physical order)
CREATE CLUSTERED INDEX IX_Employees_EmployeeID ON Employees(EmployeeID);

-- Nonclustered index (additional indexes)
CREATE NONCLUSTERED INDEX IX_Employees_LastName ON Employees(LastName);

-- Filtered index (on subset of data)
CREATE NONCLUSTERED INDEX IX_Employees_Active ON Employees(Department)
WHERE Active = 1;

-- Columnstore index (for analytics)
CREATE COLUMNSTORE INDEX IX_Employees_ColumnStore ON Employees(EmployeeID, Department, Salary);
```

### 67. What is the difference between clustered and nonclustered indexes?
**Answer:**
```sql
-- Clustered:
-- - Only one per table
-- - Determines physical storage order
-- - Faster for range queries
-- - Leaf nodes contain the actual data

-- Nonclustered:
-- - Multiple per table
-- - Doesn't affect physical order
-- - Contains pointers to actual data
-- - Slower for range queries
```

### 68. How do you optimize queries with indexes?
**Answer:**
```sql
-- 1. Identify slow queries with execution plans
-- 2. Look for table scans (instead of seeks)
-- 3. Create appropriate indexes on filtered/sorted/joined columns
-- 4. Consider included columns for covering indexes
CREATE NONCLUSTERED INDEX IX_Employees_Department
ON Employees(Department)
INCLUDE (FirstName, LastName, Salary);

-- 5. Monitor index usage and remove unused indexes
SELECT * FROM sys.dm_db_index_usage_stats;
```

### 69. What is a covering index?
**Answer:**
```sql
-- An index that includes all columns needed for a query
-- Example query:
SELECT EmployeeID, FirstName, LastName
FROM Employees
WHERE Department = 'IT';

-- Covering index:
CREATE NONCLUSTERED INDEX IX_Employees_Department_Covering
ON Employees(Department)
INCLUDE (EmployeeID, FirstName, LastName);
```

### 70. How do you use the MERGE statement?
**Answer:**
```sql
-- Perform insert/update/delete in a single statement
MERGE INTO TargetTable AS target
USING SourceTable AS source
ON target.ID = source.ID
WHEN MATCHED AND target.Value <> source.Value THEN
    UPDATE SET target.Value = source.Value
WHEN MATCHED AND source.Status = 'Deleted' THEN
    DELETE
WHEN NOT MATCHED BY TARGET THEN
    INSERT (ID, Value) VALUES (source.ID, source.Value)
WHEN NOT MATCHED BY SOURCE THEN
    DELETE;
```

## Expert Level Questions (71-100)

### 71. What are partitioned tables?
**Answer:**
```sql
-- 1. Create partition function
CREATE PARTITION FUNCTION pf_OrderDateRange (DATE)
AS RANGE RIGHT FOR VALUES 
('2020-01-01', '2021-01-01', '2022-01-01');

-- 2. Create partition scheme
CREATE PARTITION SCHEME ps_OrderDateRange
AS PARTITION pf_OrderDateRange
TO (fg_2019, fg_2020, fg_2021, fg_2022);

-- 3. Create partitioned table
CREATE TABLE Orders (
    OrderID INT,
    OrderDate DATE,
    CustomerID INT,
    Amount DECIMAL(10,2)
) ON ps_OrderDateRange(OrderDate);

-- Query partition information
SELECT $PARTITION.pf_OrderDateRange(OrderDate) AS PartitionNumber,
       COUNT(*) AS Rows
FROM Orders
GROUP BY $PARTITION.pf_OrderDateRange(OrderDate)
ORDER BY PartitionNumber;
```

### 72. What are columnstore indexes?
**Answer:**
```sql
-- Create columnstore index for analytics workloads
CREATE CLUSTERED COLUMNSTORE INDEX CCI_Orders ON Orders;

-- Nonclustered columnstore index
CREATE NONCLUSTERED COLUMNSTORE INDEX NCCI_OrderDetails 
ON OrderDetails(OrderID, ProductID, Quantity, UnitPrice);

-- Columnstore indexes:
-- - Store data column-wise instead of row-wise
-- - Excellent compression
-- - Batch mode processing
-- - Ideal for data warehouse queries
```

### 73. How do you use temporal tables?
**Answer:**
```sql
-- Create system-versioned temporal table
CREATE TABLE Employees
(
    EmployeeID INT PRIMARY KEY,
    FirstName NVARCHAR(50) NOT NULL,
    LastName NVARCHAR(50) NOT NULL,
    Department NVARCHAR(50),
    ValidFrom DATETIME2 GENERATED ALWAYS AS ROW START,
    ValidTo DATETIME2 GENERATED ALWAYS AS ROW END,
    PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)
)
WITH (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.EmployeesHistory));

-- Query current data
SELECT * FROM Employees;

-- Query historical data
SELECT * FROM Employees FOR SYSTEM_TIME AS OF '2022-01-01';

-- Query all changes for an employee
SELECT * FROM Employees 
FOR SYSTEM_TIME BETWEEN '2021-01-01' AND '2022-01-01'
WHERE EmployeeID = 1;
```

### 74. What are memory-optimized tables?
**Answer:**
```sql
-- 1. Create memory-optimized filegroup
ALTER DATABASE MyDB 
ADD FILEGROUP MemoryOptimizedFG CONTAINS MEMORY_OPTIMIZED_DATA;

-- 2. Add file to filegroup
ALTER DATABASE MyDB 
ADD FILE (NAME='MemoryOptimizedFile', FILENAME='C:\Data\MemoryOptimizedFile')
TO FILEGROUP MemoryOptimizedFG;

-- 3. Create memory-optimized table
CREATE TABLE dbo.SessionData
(
    SessionID NVARCHAR(64) NOT NULL PRIMARY KEY NONCLUSTERED,
    UserID INT NOT NULL,
    CreatedDate DATETIME2 NOT NULL,
    Data NVARCHAR(MAX)
) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA);

-- Memory-optimized tables:
-- - Reside entirely in memory
-- - No locks or latches
-- - Optimistic concurrency control
-- - Great for high-throughput OLTP
```

### 75. How do you use natively compiled stored procedures?
**Answer:**
```sql
CREATE PROCEDURE dbo.usp_InsertSession
    @SessionID NVARCHAR(64),
    @UserID INT,
    @Data NVARCHAR(MAX)
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER
AS
BEGIN ATOMIC WITH
(
    TRANSACTION ISOLATION LEVEL = SNAPSHOT,
    LANGUAGE = 'us_english'
)
    INSERT INTO dbo.SessionData (SessionID, UserID, CreatedDate, Data)
    VALUES (@SessionID, @UserID, GETUTCDATE(), @Data);
END;
```

### 76. What are graph tables in SQL Server?
**Answer:**
```sql
-- Node table
CREATE TABLE Person (
    ID INT PRIMARY KEY,
    Name NVARCHAR(50)
) AS NODE;

-- Edge table
CREATE TABLE Friends (
    Since DATE
) AS EDGE;

-- Insert nodes
INSERT INTO Person VALUES (1, 'John'), (2, 'Jane'), (3, 'Mike');

-- Insert edges (relationships)
INSERT INTO Friends VALUES 
((SELECT $node_id FROM Person WHERE ID = 1), 
 (SELECT $node_id FROM Person WHERE ID = 2), '2020-01-01'),
((SELECT $node_id FROM Person WHERE ID = 2), 
 (SELECT $node_id FROM Person WHERE ID = 3), '2021-01-01');

-- Query graph data
SELECT p1.Name AS Person1, p2.Name AS Person2, f.Since
FROM Person p1, Friends f, Person p2
WHERE MATCH(p1-(f)->p2);
```

### 77. How do you use dynamic SQL?
**Answer:**
```sql
-- Basic dynamic SQL
DECLARE @sql NVARCHAR(MAX);
DECLARE @table NVARCHAR(50) = 'Employees';
DECLARE @column NVARCHAR(50) = 'FirstName';
DECLARE @value NVARCHAR(50) = 'John';

SET @sql = N'SELECT * FROM ' + QUOTENAME(@table) + 
           N' WHERE ' + QUOTENAME(@column) + N' = @value';

EXEC sp_executesql @sql, N'@value NVARCHAR(50)', @value = @value;

-- Safer with parameterized queries
DECLARE @sql NVARCHAR(MAX) = N'
SELECT 
    e.EmployeeID,
    e.FirstName,
    e.LastName,
    d.DepartmentName
FROM Employees e
JOIN Departments d ON e.DepartmentID = d.DepartmentID
WHERE e.Salary > @minSalary';

DECLARE @minSalary DECIMAL(10,2) = 50000;

EXEC sp_executesql @sql, N'@minSalary DECIMAL(10,2)', @minSalary = @minSalary;
```

### 78. How do you prevent SQL injection?
**Answer:**
```sql
-- 1. Use parameterized queries
DECLARE @sql NVARCHAR(MAX) = N'SELECT * FROM Employees WHERE EmployeeID = @id';
DECLARE @id INT = 1;
EXEC sp_executesql @sql, N'@id INT', @id;

-- 2. Use QUOTENAME for object names
DECLARE @table NVARCHAR(128) = 'Employees';
SET @sql = N'SELECT * FROM ' + QUOTENAME(@table);
EXEC sp_executesql @sql;

-- 3. Validate input
-- 4. Use least privilege for database users
-- 5. Avoid concatenating user input directly into SQL
```

### 79. What are SQL Server Agent jobs?
**Answer:**
```sql
-- Create a job programmatically
USE msdb;
GO

EXEC dbo.sp_add_job
    @job_name = N'Nightly Data Processing';

EXEC sp_add_jobstep
    @job_name = N'Nightly Data Processing',
    @step_name = N'Process Orders',
    @subsystem = N'TSQL',
    @command = N'EXEC dbo.ProcessOrders;',
    @database_name = N'MyDB';

EXEC dbo.sp_add_schedule
    @schedule_name = N'Nightly',
    @freq_type = 4, -- Daily
    @freq_interval = 1,
    @active_start_time = 010000; -- 1:00 AM

EXEC sp_attach_schedule
    @job_name = N'Nightly Data Processing',
    @schedule_name = N'Nightly';

EXEC dbo.sp_add_jobserver
    @job_name = N'Nightly Data Processing';
```

### 80. How do you monitor query performance?
**Answer:**
```sql
-- 1. Use execution plans
SET STATISTICS IO, TIME ON;

-- 2. Query DMVs
SELECT 
    qs.execution_count,
    qs.total_logical_reads/qs.execution_count AS avg_logical_reads,
    qs.total_elapsed_time/qs.execution_count AS avg_elapsed_time,
    SUBSTRING(qt.text, (qs.statement_start_offset/2)+1,
        ((CASE qs.statement_end_offset
          WHEN -1 THEN DATALENGTH(qt.text)
         ELSE qs.statement_end_offset
         END - qs.statement_start_offset)/2)+1) AS query_text,
    qp.query_plan
FROM sys.dm_exec_query_stats AS qs
CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) AS qt
CROSS APPLY sys.dm_exec_query_plan(qs.plan_handle) AS qp
ORDER BY qs.total_logical_reads DESC;

-- 3. Use Query Store
ALTER DATABASE MyDB SET QUERY_STORE = ON;
```

### 81. How do you use Extended Events?
**Answer:**
```sql
-- Create an Extended Events session
CREATE EVENT SESSION [SlowQueries] ON SERVER 
ADD EVENT sqlserver.sql_statement_completed
(
    WHERE ([duration] > 1000000) -- 1 second
)
ADD TARGET package0.event_file(SET filename=N'SlowQueries')
WITH (MAX_MEMORY=4096 KB, MAX_DISPATCH_LATENCY=30 SECONDS);

-- Start the session
ALTER EVENT SESSION [SlowQueries] ON SERVER STATE = START;

-- Query the data
SELECT 
    event_data.value('(event/@name)[1]', 'varchar(50)') AS event_name,
    event_data.value('(event/data[@name="duration"]/value)[1]', 'bigint') AS duration,
    event_data.value('(event/data[@name="statement"]/value)[1]', 'nvarchar(max)') AS statement
FROM 
(
    SELECT CAST(event_data AS XML) AS event_data
    FROM sys.fn_xe_file_target_read_file('SlowQueries*.xel', NULL, NULL, NULL)
) AS events;
```

### 82. What are Always Encrypted columns?
**Answer:**
```sql
-- 1. Create a table with encrypted columns
CREATE TABLE Patients
(
    PatientID INT PRIMARY KEY,
    FirstName NVARCHAR(50) COLLATE Latin1_General_BIN2 
        ENCRYPTED WITH (ENCRYPTION_TYPE = DETERMINISTIC, 
                       ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256', 
                       COLUMN_ENCRYPTION_KEY = CEK1),
    LastName NVARCHAR(50) COLLATE Latin1_General_BIN2 
        ENCRYPTED WITH (ENCRYPTION_TYPE = DETERMINISTIC, 
                       ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256', 
                       COLUMN_ENCRYPTION_KEY = CEK1),
    SSN NVARCHAR(11) COLLATE Latin1_General_BIN2 
        ENCRYPTED WITH (ENCRYPTION_TYPE = RANDOMIZED, 
                       ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256', 
                       COLUMN_ENCRYPTION_KEY = CEK1),
    BirthDate DATE 
        ENCRYPTED WITH (ENCRYPTION_TYPE = RANDOMIZED, 
                       ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256', 
                       COLUMN_ENCRYPTION_KEY = CEK1)
);

-- 2. To query encrypted columns, the application must use a connection 
--    with Column Encryption Setting=enabled and have access to the column master key
```

### 83. What are Row-Level Security (RLS) policies?
**Answer:**
```sql
-- 1. Create predicate function
CREATE FUNCTION dbo.fn_securitypredicate(@Department AS NVARCHAR(50))
RETURNS TABLE
WITH SCHEMABINDING
AS
RETURN SELECT 1 AS fn_securitypredicate_result
WHERE @Department = USER_NAME() OR USER_NAME() = 'dbo';

-- 2. Create security policy
CREATE SECURITY POLICY dbo.DepartmentFilter
ADD FILTER PREDICATE dbo.fn_securitypredicate(Department) 
ON dbo.Employees;

-- Now users will only see rows where Department = their username
-- or if they're the dbo user
```

### 84. What are Dynamic Data Masking (DDM) policies?
**Answer:**
```sql
-- Add data masking to a table
ALTER TABLE Customers
ALTER COLUMN Email ADD MASKED WITH (FUNCTION = 'email()');

ALTER TABLE Customers
ALTER COLUMN CreditCardNumber ADD MASKED WITH (FUNCTION = 'partial(0, "XXXX-XXXX-XXXX-", 4)');

ALTER TABLE Customers
ALTER COLUMN Salary ADD MASKED WITH (FUNCTION = 'random(1000, 5000)');

-- Users without UNMASK permission will see masked data
-- To grant unmask permission:
GRANT UNMASK TO SomeUser;
```

### 85. How do you use change data capture (CDC)?
**Answer:**
```sql
-- Enable CDC on database
EXEC sys.sp_cdc_enable_db;

-- Enable CDC on table
EXEC sys.sp_cdc_enable_table
    @source_schema = 'dbo',
    @source_name = 'Employees',
    @role_name = 'CDC_Reader';

-- Query changes
DECLARE @from_lsn BINARY(10) = sys.fn_cdc_get_min_lsn('dbo_Employees');
DECLARE @to_lsn BINARY(10) = sys.fn_cdc_get_max_lsn();

SELECT * FROM cdc.fn_cdc_get_all_changes_dbo_Employees(
    @from_lsn, @to_lsn, 'all');
```

### 86. How do you use temporal tables with history retention?
**Answer:**
```sql
-- Create temporal table with retention
CREATE TABLE Employees
(
    EmployeeID INT PRIMARY KEY,
    FirstName NVARCHAR(50) NOT NULL,
    LastName NVARCHAR(50) NOT NULL,
    Department NVARCHAR(50),
    ValidFrom DATETIME2 GENERATED ALWAYS AS ROW START,
    ValidTo DATETIME2 GENERATED ALWAYS AS ROW END,
    PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)
)
WITH 
(
    SYSTEM_VERSIONING = ON 
    (
        HISTORY_TABLE = dbo.EmployeesHistory,
        HISTORY_RETENTION_PERIOD = 1 YEARS
    )
);

-- Clean up old history
ALTER TABLE Employees SET (SYSTEM_VERSIONING = OFF);
DELETE FROM EmployeesHistory 
WHERE ValidTo < DATEADD(YEAR, -1, GETUTCDATE());
ALTER TABLE Employees SET (SYSTEM_VERSIONING = ON 
    (HISTORY_TABLE = dbo.EmployeesHistory));
```

### 87. How do you use query hints?
**Answer:**
```sql
-- Force a specific join type
SELECT e.FirstName, d.DepartmentName
FROM Employees e WITH (NOLOCK)
INNER JOIN Departments d WITH (FORCESEEK)
    ON e.DepartmentID = d.DepartmentID
OPTION (OPTIMIZE FOR UNKNOWN, MAXDOP 4);

-- Common hints:
-- - NOLOCK (dirty reads)
-- - FORCESEEK (force index seek)
-- - INDEX (force specific index)
-- - OPTIMIZE FOR (optimize for specific parameter)
-- - MAXDOP (limit parallelism)
-- - RECOMPILE (force recompile)
```

### 88. How do you use plan guides?
**Answer:**
```sql
-- Create plan guide to force a specific plan
EXEC sp_create_plan_guide
    @name = N'ForceSeekOnEmployeeQuery',
    @stmt = N'SELECT * FROM Employees WHERE Department = @dept',
    @type = N'SQL',
    @module_or_batch = NULL,
    @params = N'@dept NVARCHAR(50)',
    @hints = N'OPTION (OPTIMIZE FOR (@dept = N''IT''), FORCESEEK)';

-- Verify plan guide
SELECT * FROM sys.plan_guides;

-- Disable/enable plan guide
EXEC sp_control_plan_guide N'DISABLE', N'ForceSeekOnEmployeeQuery';
EXEC sp_control_plan_guide N'ENABLE', N'ForceSeekOnEmployeeQuery';

-- Drop plan guide
EXEC sp_control_plan_guide N'DROP', N'ForceSeekOnEmployeeQuery';
```

### 89. How do you use Resource Governor?
**Answer:**
```sql
-- 1. Create resource pool
CREATE RESOURCE POOL ReportingPool
WITH (
    MIN_CPU_PERCENT = 20,
    MAX_CPU_PERCENT = 50,
    MIN_MEMORY_PERCENT = 20,
    MAX_MEMORY_PERCENT = 50
);

-- 2. Create workload group
CREATE WORKLOAD GROUP ReportingGroup
USING ReportingPool;

-- 3. Create classifier function
CREATE FUNCTION dbo.rgClassifier()
RETURNS SYSNAME
WITH SCHEMABINDING
AS
BEGIN
    DECLARE @group SYSNAME;
    
    IF APP_NAME() LIKE '%Report%'
        SET @group = 'ReportingGroup';
    ELSE
        SET @group = 'default';
    
    RETURN @group;
END;
GO

-- 4. Configure Resource Governor
ALTER RESOURCE GOVERNOR WITH (CLASSIFIER_FUNCTION = dbo.rgClassifier);
ALTER RESOURCE GOVERNOR RECONFIGURE;
```

### 90. How do you use PolyBase?
**Answer:**
```sql
-- Configure PolyBase to query external data sources
-- 1. Enable PolyBase
EXEC sp_configure @configname = 'polybase enabled', @configvalue = 1;
RECONFIGURE;

-- 2. Create external data source (e.g., SQL Server)
CREATE EXTERNAL DATA SOURCE RemoteSQLServer
WITH (
    LOCATION = 'sqlserver://remote-server.database.windows.net',
    CREDENTIAL = RemoteDBCredential
);

-- 3. Create external table
CREATE EXTERNAL TABLE dbo.RemoteEmployees
(
    EmployeeID INT,
    FirstName NVARCHAR(50),
    LastName NVARCHAR(50)
)
WITH (
    DATA_SOURCE = RemoteSQLServer,
    SCHEMA_NAME = 'dbo',
    OBJECT_NAME = 'Employees'
);

-- 4. Query external data
SELECT * FROM dbo.RemoteEmployees;
```

### 91. How do you use In-Memory OLTP?
**Answer:**
```sql
-- 1. Add memory-optimized filegroup (see question 74)
-- 2. Create memory-optimized table
CREATE TABLE dbo.ShoppingCart
(
    CartID NVARCHAR(50) NOT NULL PRIMARY KEY NONCLUSTERED,
    UserID INT NOT NULL,
    CreatedDate DATETIME2 NOT NULL,
    INDEX ix_UserID NONCLUSTERED HASH (UserID) WITH (BUCKET_COUNT = 1000000)
) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA);

-- 3. Create natively compiled stored procedure (see question 75)
-- 4. Use for high-throughput OLTP workloads
```

### 92. How do you use sp_WhoIsActive?
**Answer:**
```sql
-- sp_WhoIsActive is a popular diagnostic stored procedure
-- Download from: http://whoisactive.com/

-- Basic usage
EXEC sp_WhoIsActive;

-- With additional details
EXEC sp_WhoIsActive 
    @get_plans = 1,
    @get_outer_command = 1,
    @get_transaction_info = 1,
    @get_locks = 1;

-- Filter by database
EXEC sp_WhoIsActive @filter_type = 'database', @filter = 'MyDB';

-- Find blocking chains
EXEC sp_WhoIsActive @find_block_leaders = 1;
```

### 93. How do you use Database Tuning Advisor (DTA)?
**Answer:**
```sql
-- 1. Capture workload (SQL Server Profiler or Extended Events)
-- 2. Run DTA against workload
-- Command-line example:
dta -E -D MyDB -if Workload.sql -of Recommendations.sql -F -ix

-- Or programmatically:
DECLARE @handle UNIQUEIDENTIFIER;
DECLARE @xml NVARCHAR(MAX);

-- Start tuning session
EXEC sp_DTA_start_session @handle OUTPUT;

-- Add workload file
EXEC sp_DTA_add_file_workload @handle, 'C:\Workload.sql';

-- Set tuning options
EXEC sp_DTA_set_tuning_options 
    @handle,
    @storage_size = 1000,
    @max_columns_in_index = 16,
    @online_index = 'ON';

-- Execute tuning
EXEC sp_DTA_execute_tuning_session @handle;

-- Get recommendations
EXEC sp_DTA_get_recommendations @handle, @xml OUTPUT;

-- Display recommendations
SELECT @xml AS Recommendations;

-- Close session
EXEC sp_DTA_close_session @handle;
```

### 94. How do you use Query Store hints?
**Answer:**
```sql
-- 1. Find query_id in Query Store
SELECT q.query_id, t.query_sql_text
FROM sys.query_store_query q
JOIN sys.query_store_query_text t ON q.query_text_id = t.query_text_id
WHERE t.query_sql_text LIKE '%Employees%';

-- 2. Apply hint (SQL Server 2022+)
EXEC sys.sp_query_store_set_hints 
    @query_id = 123,
    @query_hints = 'OPTION (OPTIMIZE FOR UNKNOWN, MAXDOP 4)';

-- 3. Verify hint
SELECT query_id, query_hints
FROM sys.query_store_query_hints
WHERE query_id = 123;

-- 4. Remove hint
EXEC sys.sp_query_store_clear_hints @query_id = 123;
```

### 95. How do you use ledger tables?
**Answer:**
```sql
-- Create ledger table (SQL Server 2022+)
CREATE TABLE AccountBalances
(
    AccountID INT PRIMARY KEY,
    Balance DECIMAL(10,2) NOT NULL
) WITH (LEDGER = ON);

-- Insert data (generates history automatically)
INSERT INTO AccountBalances VALUES (1, 1000.00);

-- Update data (history tracked)
UPDATE AccountBalances SET Balance = 1500.00 WHERE AccountID = 1;

-- Query current data
SELECT * FROM AccountBalances;

-- Query history
SELECT * FROM AccountBalances_Ledger;

-- Verify data integrity
DECLARE @digest_locations NVARCHAR(MAX) = 
    (SELECT * FROM sys.database_ledger_digest_locations FOR JSON AUTO);
EXEC sys.sp_verify_database_ledger @digest_locations;
```

### 96. How do you use containment in SQL Server?
**Answer:**
```sql
-- 1. Make database partially contained
ALTER DATABASE MyDB SET CONTAINMENT = PARTIAL;

-- 2. Create contained user
CREATE USER ContainedUser WITH PASSWORD = 'StrongPassword';

-- 3. Now user can connect directly to this database without server login
-- Benefits:
-- - Easier database movement
-- - No dependency on server logins
-- - Better isolation

-- Check containment
SELECT containment, containment_desc 
FROM sys.databases 
WHERE name = 'MyDB';
```

### 97. How do you use Always On Availability Groups?
**Answer:**
```sql
-- 1. Enable Always On on each server instance
-- 2. Create availability group
CREATE AVAILABILITY GROUP [AG_MyDB]
WITH (
    AUTOMATED_BACKUP_PREFERENCE = SECONDARY,
    FAILOVER_MODE = AUTOMATIC,
    HEALTH_CHECK_TIMEOUT = 30000
)
FOR DATABASE [MyDB]
REPLICA ON 
    'PrimaryServer' WITH (
        ENDPOINT_URL = 'TCP://PrimaryServer:5022',
        AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
        FAILOVER_MODE = AUTOMATIC,
        BACKUP_PRIORITY = 50,
        SECONDARY_ROLE(ALLOW_CONNECTIONS = READ_ONLY)
    ),
    'SecondaryServer' WITH (
        ENDPOINT_URL = 'TCP://SecondaryServer:5022',
        AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
        FAILOVER_MODE = AUTOMATIC,
        BACKUP_PRIORITY = 50,
        SECONDARY_ROLE(ALLOW_CONNECTIONS = READ_ONLY)
    );

-- 3. Join secondary replicas
-- On secondary server:
ALTER AVAILABILITY GROUP [AG_MyDB] JOIN;
ALTER AVAILABILITY GROUP [AG_MyDB] GRANT CREATE ANY DATABASE;

-- 4. Query AG status
SELECT 
    ag.name AS AGName,
    ar.replica_server_name,
    ars.connected_state_desc,
    ars.synchronization_health_desc
FROM sys.availability_groups ag
JOIN sys.availability_replicas ar ON ag.group_id = ar.group_id
JOIN sys.dm_hadr_availability_replica_states ars 
    ON ar.replica_id = ars.replica_id;
```

### 98. How do you use distributed queries?
**Answer:**
```sql
-- 1. Configure linked server
EXEC sp_addlinkedserver
    @server = 'RemoteServer',
    @srvproduct = 'SQL Server';

EXEC sp_addlinkedsrvlogin
    @rmtsrvname = 'RemoteServer',
    @useself = 'false',
    @locallogin = NULL,
    @rmtuser = 'remoteuser',
    @rmtpassword = 'password';

-- 2. Query remote data
SELECT * FROM RemoteServer.MyDB.dbo.Employees;

-- 3. Join local and remote data
SELECT l.EmployeeID, r.SalesAmount
FROM LocalEmployees l
JOIN RemoteServer.MyDB.dbo.Sales r ON l.EmployeeID = r.EmployeeID;

-- 4. Use OPENQUERY for better performance
SELECT * FROM OPENQUERY(RemoteServer, 'SELECT * FROM MyDB.dbo.Employees');
```

### 99. How do you use BULK INSERT?
**Answer:**
```sql
-- Simple bulk insert
BULK INSERT Employees
FROM 'C:\Data\employees.csv'
WITH (
    FIELDTERMINATOR = ',',
    ROWTERMINATOR = '\n',
    FIRSTROW = 2
);

-- Advanced options
BULK INSERT Employees
FROM 'C:\Data\employees.csv'
WITH (
    DATAFILETYPE = 'char',
    FIELDTERMINATOR = '|',
    ROWTERMINATOR = '0x0a',
    FIRSTROW = 2,
    KEEPIDENTITY,
    TABLOCK,
    ERRORFILE = 'C:\Data\errors.log',
    MAXERRORS = 100
);

-- With format file
BULK INSERT Employees
FROM 'C:\Data\employees.dat'
WITH (
    FORMATFILE = 'C:\Data\employees.fmt'
);
```

### 100. How do you use SQLCLR?
**Answer:**
```sql
-- 1. Enable CLR
sp_configure 'clr enabled', 1;
RECONFIGURE;

-- 2. Create assembly from DLL
CREATE ASSEMBLY MyCLRFunctions
FROM 'C:\CLR\MyCLRFunctions.dll'
WITH PERMISSION_SET = SAFE;

-- 3. Create CLR function
CREATE FUNCTION dbo.CLR_RegexMatch
(
    @input NVARCHAR(MAX),
    @pattern NVARCHAR(100)
)
RETURNS BIT
AS EXTERNAL NAME MyCLRFunctions.UserDefinedFunctions.RegexMatch;

-- 4. Use the function
SELECT dbo.CLR_RegexMatch(Email, '^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,4}$') 
FROM Customers;

-- Security considerations:
-- - Use SAFE permission set when possible
-- - Sign assemblies with certificates
-- - Consider alternatives like T-SQL or built-in functions
```
