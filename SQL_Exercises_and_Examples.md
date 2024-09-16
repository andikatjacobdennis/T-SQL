| **Topic** | **Practice Question** | **T-SQL Answer** |
|-----------|------------------------|------------------|
| **Database Creation & Management** | Create a new database called `SalesDB`. | `CREATE DATABASE SalesDB;` |
| | Select and use the `SalesDB` database. | `USE SalesDB;` |
| | List all available databases on the server. | `SHOW DATABASES;` |
| | Rename `OldSalesDB` to `NewSalesDB`. | `ALTER DATABASE OldSalesDB MODIFY NAME = NewSalesDB;` |
| | Backup the `SalesDB` database. | `BACKUP DATABASE SalesDB TO DISK = 'C:\Backup\SalesDB.bak';` |
| | Restore the `SalesDB` database. | `RESTORE DATABASE SalesDB FROM DISK = 'C:\Backup\SalesDB.bak' WITH REPLACE;` |
| | Drop the database `TestDB`. | `DROP DATABASE TestDB;` |
| **Table Creation & Management** | Create a `Products` table with `ProductID` as the primary key, `ProductName` as unique, `Price` not null, and `Category` with a check constraint. | ```CREATE TABLE Products ( ProductID INT PRIMARY KEY, ProductName NVARCHAR(100) UNIQUE, Price DECIMAL(10, 2) NOT NULL, Category NVARCHAR(50) CHECK (Category IN ('Electronics', 'Clothing', 'Food', 'Furniture')) ); ``` |
| | Create a temporary table for storing product sales during a session. | ```CREATE TABLE #TempSales ( SaleID INT, ProductID INT, SaleAmount DECIMAL(10, 2) ); ``` |
| | Rename the table `OldProducts` to `NewProducts`. | ```EXEC sp_rename 'OldProducts', 'NewProducts'; ``` |
| | Add a new column `StockQuantity` to the `Products` table. | ```ALTER TABLE Products ADD StockQuantity INT; ``` |
| | Create a composite key on the `ProductID` and `OrderID` columns in the `OrderDetails` table. | `ALTER TABLE OrderDetails ADD CONSTRAINT PK_ProductOrder PRIMARY KEY (ProductID, OrderID);` |
| | Add a foreign key constraint to the `Sales` table referencing `Products`. | ```ALTER TABLE Sales ADD CONSTRAINT FK_Product FOREIGN KEY (ProductID) REFERENCES Products(ProductID); ``` |
| | Add a unique key constraint on the `ProductName` column in the `Products` table. | ```ALTER TABLE Products ADD CONSTRAINT UQ_ProductName UNIQUE (ProductName); ``` |
| | Drop the unique key constraint on the `ProductName` column. | ```ALTER TABLE Products DROP CONSTRAINT UQ_ProductName; ``` |
| | Truncate all records from the `Sales` table. | ```TRUNCATE TABLE Sales; ``` |
| | Permanently delete the `OldProducts` table. | ```DROP TABLE OldProducts; ``` |
| | Drop the `#TempSales` table. | ```DROP TABLE #TempSales; ``` |
| **Data Manipulation** | Insert a new product into the `Products` table with name 'Smartphone' and price 299. | `INSERT INTO Products (ProductID, ProductName, Price, Category) VALUES (1, 'Smartphone', 299, 'Electronics');` |
| | Update the price of the product 'Smartphone' to 350. | `UPDATE Products SET Price = 350 WHERE ProductName = 'Smartphone';` |
| | Delete all products where the price is below 10. | `DELETE FROM Products WHERE Price < 10;` |
| **Querying & Data Retrieval** | Retrieve all product names and their prices from the `Products` table. | `SELECT ProductName, Price FROM Products;` |
| | Insert all records from the `Products` table into a new table called `BackupProducts`. | `SELECT * INTO BackupProducts FROM Products;` |
| | Retrieve the top 5 most expensive products. | `SELECT TOP 5 * FROM Products ORDER BY Price DESC;` |
| | Retrieve the distinct product categories from the `Products` table. | `SELECT DISTINCT Category FROM Products;` |
| | Use COALESCE to return the first non-null value from a list. | `SELECT ProductName, COALESCE(Price, 0) AS Price FROM Products;` |
| | Retrieve all products and replace any NULL price values with 0. | `SELECT ProductName, ISNULL(Price, 0) AS Price FROM Products;` |
| | Retrieve all products where the price is greater than 50. | `SELECT * FROM Products WHERE Price > 50;` |
| | Retrieve all sales where the sale amount is between 100 and 500. | `SELECT * FROM Sales WHERE SaleAmount BETWEEN 100 AND 500;` |
| | Retrieve all products where the category is either 'Electronics' or 'Clothing'. | `SELECT * FROM Products WHERE Category = 'Electronics' OR Category = 'Clothing';` |
| | Retrieve all products that are not in the 'Clothing' category. | `SELECT * FROM Products WHERE Category <> 'Clothing';` |
| | Retrieve all product names that start with the letter 'S'. | `SELECT ProductName FROM Products WHERE ProductName LIKE 'S%';` |
| **Aggregations and Grouping** | Find the total sales amount from the `Sales` table. | `SELECT SUM(SaleAmount) AS TotalSales FROM Sales;` |
| | Retrieve the minimum and maximum product prices. | `SELECT MIN(Price) AS MinPrice, MAX(Price) AS MaxPrice FROM Products;` |
| | Count the total number of products in the `Products` table. | `SELECT COUNT(*) AS TotalProducts FROM Products;` |
| | Find the average price of all products. | `SELECT AVG(Price) AS AveragePrice FROM Products;` |
| | Group all products by category and count how many products exist in each category. | `SELECT Category, COUNT(*) AS ProductCount FROM Products GROUP BY Category;` |
| | Retrieve product categories having more than 5 products. | `SELECT Category FROM Products GROUP BY Category HAVING COUNT(*) > 5;` |
| | Retrieve all customers where the `phone_number` is NULL. | `SELECT * FROM Customers WHERE phone_number IS NULL;` |
| **Joins & Set Operations** | Retrieve all sales with the corresponding product name by joining `Sales` and `Products` tables. | `SELECT Sales.*, Products.ProductName FROM Sales INNER JOIN Products ON Sales.ProductID = Products.ProductID;` |
| | Retrieve the customer name and the corresponding sales amount by joining `Customers` and `Sales` tables. | `SELECT Customers.CustomerName, Sales.SaleAmount FROM Sales INNER JOIN Customers ON Sales.CustomerID = Customers.CustomerID;` |
| | Retrieve all products and their sales data, showing NULL for products that haven’t been sold. | `SELECT Products.ProductName, Sales.SaleAmount FROM Products LEFT JOIN Sales ON Products.ProductID = Sales.ProductID;` |
| | Retrieve all sales and the product details, showing NULL for products that no longer exist. | `SELECT Sales.SaleID, Products.ProductName FROM Sales RIGHT JOIN Products ON Sales.ProductID = Products.ProductID;` |
| | Retrieve all products and their sales information, even if there is no match on either side. | `SELECT Products.ProductName, Sales.SaleAmount FROM Products FULL JOIN Sales ON Products.ProductID = Sales.ProductID;` |
| | Retrieve all products that have the same price by joining the `Products` table to itself. | `SELECT A.ProductName, B.ProductName FROM Products A INNER JOIN Products B ON A.Price = B.Price AND A.ProductID <> B.ProductID;` |
| | Retrieve all distinct product names from `Products` and `Sales` tables. | `SELECT DISTINCT ProductName FROM Products UNION SELECT DISTINCT ProductName FROM Sales;` |
| **Subqueries and Advanced Queries** | Retrieve all customers who have made a purchase. | `SELECT DISTINCT CustomerID FROM Sales;` |
| | Retrieve all products where the price is greater than all products in the 'Clothing' category. | `SELECT * FROM Products WHERE Price > ALL (SELECT Price FROM Products WHERE Category = 'Clothing');` |
| | Retrieve all products and add a new column showing 'Expensive' if the price is above 100, otherwise 'Cheap'. | `SELECT ProductName, Price, CASE WHEN Price > 100 THEN 'Expensive' ELSE 'Cheap' END AS PriceCategory FROM Products;` |
| **Indexes** | Create an index on the `ProductName` column for faster searches. | `CREATE INDEX idx_ProductName ON Products (ProductName);` |
| | Create an index on the `SaleDate` column in the `Sales` table. | `CREATE INDEX idx_SaleDate ON Sales (SaleDate);` |
| | Drop the index on the `ProductName` column. | `DROP INDEX idx_ProductName ON Products;` |
| | Retrieve all indexes on the `Products` table. | `SELECT * FROM sys.indexes WHERE object_id = OBJECT_ID('Products');` |
| | Create a unique index on the `ProductCode` column in the `Products` table. | `CREATE UNIQUE INDEX idx_ProductCode ON Products (ProductCode);` |
| | Create a clustered index on the `ProductID` column in the `Products` table. | `CREATE  CLUSTERED INDEX idx_ProductID ON Products (ProductID);` |
| | Create a non-clustered index on the `ProductName` column. | `CREATE NONCLUSTERED INDEX idx_ProductName ON Products (ProductName);` |
| **Views** | Create a view that shows product names and total sales for each product. | `CREATE VIEW ProductSalesView AS SELECT Products.ProductName, SUM(Sales.SaleAmount) AS TotalSales FROM Products LEFT JOIN Sales ON Products.ProductID = Sales.ProductID GROUP BY Products.ProductName;` |
| | Update the `ProductSalesView` to include the average sale amount. | `CREATE OR ALTER VIEW ProductSalesView AS SELECT Products.ProductName, SUM(Sales.SaleAmount) AS TotalSales, AVG(Sales.SaleAmount) AS AverageSales FROM Products LEFT JOIN Sales ON Products.ProductID = Sales.ProductID GROUP BY Products.ProductName;` |
| | Drop the `ObsoleteView` from the database. | `DROP VIEW ObsoleteView;` |
| | Rename `ProductSalesView` to `ProductRevenueView`. | `EXEC sp_rename 'ProductSalesView', 'ProductRevenueView';` |
| **Stored Procedures & Functions** | Create a stored procedure to add a new sale record to the `Sales` table. | `CREATE PROCEDURE AddSale @ProductID INT, @SaleAmount DECIMAL(10, 2), @SaleDate DATE AS BEGIN INSERT INTO Sales (ProductID, SaleAmount, SaleDate) VALUES (@ProductID, @SaleAmount, @SaleDate); END;` |
| | Write a function that calculates the total sales for a given product. | `CREATE FUNCTION TotalSalesForProduct (@ProductID INT) RETURNS DECIMAL(10, 2) AS BEGIN RETURN (SELECT SUM(SaleAmount) FROM Sales WHERE ProductID = @ProductID); END;` |
| **Advanced Concepts** | Write a loop to update prices for all products that meet a specific condition. | `DECLARE @ProductID INT, @NewPrice DECIMAL(10, 2) SET @NewPrice = 100; DECLARE ProductCursor CURSOR FOR SELECT ProductID FROM Products WHERE Price < @NewPrice OPEN ProductCursor FETCH NEXT FROM ProductCursor INTO @ProductID WHILE @@FETCH_STATUS = 0 BEGIN UPDATE Products SET Price = @NewPrice WHERE ProductID = @ProductID FETCH NEXT FROM ProductCursor INTO @ProductID END CLOSE ProductCursor DEALLOCATE ProductCursor;` |
| | Create a trigger that updates the stock quantity in the `Products` table after every insert into `Sales`. | `CREATE TRIGGER UpdateStock AFTER INSERT ON Sales FOR EACH ROW BEGIN UPDATE Products SET StockQuantity = StockQuantity - 1 WHERE ProductID = NEW.ProductID; END;` |
| | Grant a user permission to view the `Products` table but revoke their ability to delete records. | `GRANT SELECT ON Products TO [username]; REVOKE DELETE ON Products FROM [username];` |
| **Transactions** | Begin a transaction for inserting a new product and updating the stock quantity. | `BEGIN TRANSACTION; INSERT INTO Products (ProductID, ProductName, Price, Category) VALUES (2, 'Tablet', 199, 'Electronics'); UPDATE Products SET StockQuantity = StockQuantity + 10 WHERE ProductID = 2; COMMIT TRANSACTION;` |
| | Rollback a transaction if an error occurs during multiple inserts. | `BEGIN TRANSACTION; BEGIN TRY INSERT INTO Products (ProductID, ProductName, Price, Category) VALUES (3, 'Laptop', 799, 'Electronics'); INSERT INTO Products (ProductID, ProductName, Price, Category) VALUES (4, 'Keyboard', 49, 'Accessories'); COMMIT TRANSACTION; END TRY BEGIN CATCH ROLLBACK TRANSACTION; END CATCH;` |
| | Save a transaction state so that it can be rolled back later. | `BEGIN TRANSACTION; INSERT INTO Products (ProductID, ProductName, Price, Category) VALUES (5, 'Mouse', 25, 'Accessories'); SAVE TRANSACTION SavePoint1; INSERT INTO Products (ProductID, ProductName, Price, Category) VALUES (6, 'Monitor', 150, 'Electronics'); ROLLBACK TRANSACTION SavePoint1; COMMIT TRANSACTION;` |
| | Check the status of the current transaction. | `SELECT @@TRANCOUNT;` |
| **Error Handling** | Implement basic error handling in a query to avoid runtime errors. | `BEGIN TRY INSERT INTO Products (ProductID, ProductName, Price, Category) VALUES (1, 'Smartwatch', 199, 'Electronics'); END TRY BEGIN CATCH SELECT ERROR_MESSAGE() AS ErrorMessage; END CATCH;` |
| | Write a stored procedure that handles errors when inserting sales data. | `CREATE PROCEDURE AddSaleWithErrorHandling @ProductID INT, @SaleAmount DECIMAL(10, 2), @SaleDate DATE AS BEGIN BEGIN TRY INSERT INTO Sales (ProductID, SaleAmount, SaleDate) VALUES (@ProductID, @SaleAmount, @SaleDate); END TRY BEGIN CATCH SELECT ERROR_MESSAGE() AS ErrorMessage; ROLLBACK TRANSACTION; END CATCH END;` |
| | Capture detailed error information, including error number, severity, and state. | `BEGIN TRY -- Operation END TRY BEGIN CATCH SELECT ERROR_NUMBER(), ERROR_SEVERITY(), ERROR_STATE(), ERROR_PROCEDURE(), ERROR_LINE(), ERROR_MESSAGE(); END CATCH;` |
| **Transactions with Error Handling** | Write a query with transaction control and error handling for multiple operations. | `BEGIN TRANSACTION; BEGIN TRY INSERT INTO Products (ProductID, ProductName, Price, Category) VALUES (10, 'TV', 499, 'Electronics'); UPDATE Products SET StockQuantity = StockQuantity + 10 WHERE ProductID = 10; COMMIT TRANSACTION; END TRY BEGIN CATCH ROLLBACK TRANSACTION; SELECT ERROR_MESSAGE(); END CATCH;` |
| | Implement a transaction that rolls back after a failure in any step. | `BEGIN TRANSACTION; BEGIN TRY INSERT INTO Products (ProductID, ProductName, Price, Category) VALUES (11, 'Speaker', 150, 'Electronics'); INSERT INTO Sales (ProductID, SaleAmount, SaleDate) VALUES (11, 150, GETDATE()); COMMIT TRANSACTION; END TRY BEGIN CATCH ROLLBACK TRANSACTION; SELECT ERROR_MESSAGE(); END CATCH;` |
| | Add a SAVEPOINT to handle partial rollbacks within a transaction. | `BEGIN TRANSACTION; INSERT INTO Products (ProductID, ProductName, Price, Category) VALUES (12, 'Tablet', 250, 'Electronics'); SAVE TRANSACTION SavePoint1; INSERT INTO Products (ProductID, ProductName, Price, Category) VALUES (13, 'Headphones', 75, 'Electronics'); IF (@@ERROR <> 0) ROLLBACK TRANSACTION SavePoint1; COMMIT TRANSACTION;` |
| **Cursors** | Create a cursor to loop through all products and update prices for each product. | `DECLARE @ProductID INT, @NewPrice DECIMAL(10, 2); DECLARE ProductCursor CURSOR FOR SELECT ProductID FROM Products; OPEN ProductCursor; FETCH NEXT FROM ProductCursor INTO @ProductID; WHILE @@FETCH_STATUS = 0 BEGIN UPDATE Products SET Price = Price * 1.10 WHERE ProductID = @ProductID; FETCH NEXT FROM ProductCursor INTO @ProductID; END CLOSE ProductCursor; DEALLOCATE ProductCursor;` |
| **Common Table Expressions** | Use a CTE to retrieve the top 5 most expensive products. | `WITH ExpensiveProducts AS (SELECT ProductName, Price, ROW_NUMBER() OVER (ORDER BY Price DESC) AS RowNum FROM Products) SELECT ProductName, Price FROM ExpensiveProducts WHERE RowNum <= 5;` |
| | Use a recursive CTE to calculate the factorial of a number. | `WITH FactorialCTE AS (SELECT 1 AS N, 1 AS Factorial UNION ALL SELECT N + 1, (N + 1) * Factorial FROM FactorialCTE WHERE N < 5) SELECT * FROM FactorialCTE;` |
| **Dynamic SQL** | Write a dynamic SQL query to retrieve products based on a variable category. | `DECLARE @Category NVARCHAR(50); SET @Category = 'Electronics'; DECLARE @SQL NVARCHAR(MAX); SET @SQL = 'SELECT * FROM Products WHERE Category = ''' + @Category + ''''; EXEC sp_executesql @SQL;` |
| | Use dynamic SQL to create a query that selects data from a table specified by the user. | `DECLARE @TableName NVARCHAR(100); SET @TableName = 'Products'; DECLARE @SQL NVARCHAR(MAX); SET @SQL = 'SELECT * FROM ' + @TableName; EXEC sp_executesql @SQL;` |
| **Window Functions** | Calculate the cumulative sales amount for each product using `OVER()`. | `SELECT ProductID, SaleAmount, SUM(SaleAmount) OVER (PARTITION BY ProductID ORDER BY SaleDate) AS CumulativeSales FROM Sales;` |
| | Retrieve the rank of products based on their price. | `SELECT ProductName, Price, RANK() OVER (ORDER BY Price DESC) AS PriceRank FROM Products;` |
| **Partitioning** | Partition sales data by product category and calculate total sales in each partition. | `SELECT Category, SUM(SaleAmount) OVER (PARTITION BY Category) AS TotalSales FROM Products P INNER JOIN Sales S ON P.ProductID = S.ProductID;` |
| | Partition data and calculate row number within each partition for products. | `SELECT ProductName, Category, ROW_NUMBER() OVER (PARTITION BY Category ORDER BY Price DESC) AS RowNum FROM Products;` |
| **Full-Text Search** | Perform a full-text search for products containing the word 'Phone'. | `SELECT * FROM Products WHERE CONTAINS(ProductName, 'Phone');` |
| | Enable full-text search on the `ProductName` column and search for records containing 'Watch'. | `CREATE FULLTEXT CATALOG ftCatalog AS DEFAULT; CREATE FULLTEXT INDEX ON Products (ProductName) KEY INDEX PK_ProductID; SELECT * FROM Products WHERE CONTAINS(ProductName, 'Watch');` |
| **Pivoting** | Pivot the sales data to show total sales by product for each year. | `SELECT * FROM (SELECT ProductID, YEAR(SaleDate) AS SaleYear, SaleAmount FROM Sales) AS SourceTable PIVOT (SUM(SaleAmount) FOR SaleYear IN ([2021], [2022], [2023])) AS PivotTable;` |
| | Use `PIVOT` to display total sales for each product category. | `SELECT * FROM (SELECT Category, SaleAmount FROM Products P INNER JOIN Sales S ON P.ProductID = S.ProductID) AS SourceTable PIVOT (SUM(SaleAmount) FOR Category IN ('Electronics', 'Clothing', 'Accessories')) AS PivotTable;` |
| **Unpivoting** | Unpivot sales data to display product sales for each year in rows. | `SELECT ProductID, SaleYear, SaleAmount FROM (SELECT ProductID, [2021], [2022], [2023] FROM SalesByYear) AS PivotTable UNPIVOT (SaleAmount FOR SaleYear IN ([2021], [2022], [2023])) AS UnpivotTable;` |
| **XML Data Handling** | Create an XML column in a table to store product details. | `ALTER TABLE Products ADD ProductDetails XML;` |
| | Insert XML data into the `ProductDetails` column of the `Products` table. | `UPDATE Products SET ProductDetails = '<Product><Name>Smartphone</Name><Price>299</Price></Product>' WHERE ProductID = 1;` |
| | Query the `ProductDetails` XML column to retrieve the product name. | `SELECT ProductDetails.value('(/Product/Name)[1]', 'NVARCHAR(100)') AS ProductName FROM Products WHERE ProductID = 1;` |
| | Extract the price from the `ProductDetails` XML column. | `SELECT ProductDetails.value('(/Product/Price)[1]', 'DECIMAL(10, 2)') AS Price FROM Products WHERE ProductID = 1;` |
| | Update the `ProductDetails` XML to set a new price. | `UPDATE Products SET ProductDetails.modify('replace value of (/Product/Price/text())[1] with 350') WHERE ProductID = 1;` |
| **JSON Data Handling** | Create a column in a table to store JSON data. | `ALTER TABLE Products ADD ProductAttributes NVARCHAR(MAX);` |
| | Insert JSON data into the `ProductAttributes` column of the `Products` table. | `UPDATE Products SET ProductAttributes = '{"Color": "Black", "Warranty": "1 Year"}' WHERE ProductID = 1;` |
| | Query the `ProductAttributes` JSON column to retrieve the warranty information. | `SELECT JSON_VALUE(ProductAttributes, '$.Warranty') AS Warranty FROM Products WHERE ProductID = 1;` |
| | Extract the color from the `ProductAttributes` JSON column. | `SELECT JSON_VALUE(ProductAttributes, '$.Color') AS Color FROM Products WHERE ProductID = 1;` |
| | Update the `ProductAttributes` JSON to add a new attribute. | `UPDATE Products SET ProductAttributes = JSON_MODIFY(ProductAttributes, '$.Weight', '150g') WHERE ProductID = 1;` |
| **Views & Permissions** | Create a view to show product details and grant select permissions to a user. | CREATE VIEW vw_ProductDetails AS SELECT * FROM Products; GRANT SELECT ON vw_ProductDetails TO UserName; |
| | Revoke select permissions on the view from the user. | REVOKE SELECT ON vw_ProductDetails FROM UserName; |
| **User-Defined Functions** | Create a scalar-valued function to calculate the total price after a discount. | CREATE FUNCTION dbo.ApplyDiscount (@Price DECIMAL(10, 2), @Discount DECIMAL(5, 2)) RETURNS DECIMAL(10, 2) AS BEGIN RETURN @Price - (@Price * @Discount / 100); END; |
| | Use the function to calculate the final price with a 10% discount. | SELECT dbo.ApplyDiscount(100, 10) AS FinalPrice; |

