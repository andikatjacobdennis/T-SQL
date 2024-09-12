| **Topic** | **Practice Question** | **T-SQL Answer** |
|-----------|------------------------|------------------|
| **Database Creation & Management** | Create a new database called `SalesDB`. | `CREATE DATABASE SalesDB;` |
| | Select and use the `SalesDB` database. | `USE SalesDB;` |
| | List all available databases on the server. | `SHOW DATABASES;` |
| | Rename `OldSalesDB` to `NewSalesDB`. | `ALTER DATABASE OldSalesDB MODIFY NAME = NewSalesDB;` |
| | Backup the `SalesDB` database. | `BACKUP DATABASE SalesDB TO DISK = 'C:\Backup\SalesDB.bak';` |
| | Drop the database `TestDB`. | `DROP DATABASE TestDB;` |
| **Table Creation & Management** | Create a table `Products` with columns `ProductID`, `ProductName`, `Price`, and `Category`. | `CREATE TABLE Products (ProductID INT PRIMARY KEY, ProductName NVARCHAR(100), Price DECIMAL(10, 2), Category NVARCHAR(50));` |
| | Retrieve all tables from the `SalesDB` database. | `SELECT * FROM INFORMATION_SCHEMA.TABLES;` |
| | Add a new column `StockQuantity` to the `Products` table. | `ALTER TABLE Products ADD StockQuantity INT;` |
| | Rename the table `OldProducts` to `NewProducts`. | `EXEC sp_rename 'OldProducts', 'NewProducts';` |
| | Create a clone of the `Products` table including the schema and data. | `SELECT * INTO Products_Clone FROM Products;` |
| | Create a temporary table for storing product sales during a session. | `CREATE TABLE #TempSales (SaleID INT, ProductID INT, SaleAmount DECIMAL(10, 2));` |
| | Add a foreign key constraint to the `Sales` table referencing `Products`. | `ALTER TABLE Sales ADD CONSTRAINT FK_Product FOREIGN KEY (ProductID) REFERENCES Products(ProductID);` |
| | Truncate all records from the `Sales` table. | `TRUNCATE TABLE Sales;` |
| | Permanently delete the `OldProducts` table. | `DROP TABLE OldProducts;` |
| | Drop the `TemporarySales` table. | `DROP TABLE #TempSales;` |
| **Inserting Data into Tables** | Insert a new product into the `Products` table with name 'Smartphone' and price 299. | `INSERT INTO Products (ProductID, ProductName, Price, Category) VALUES (1, 'Smartphone', 299, 'Electronics');` |
| | Insert all records from the `Products` table into a new table called `BackupProducts`. | `SELECT * INTO BackupProducts FROM Products;` |
| | Create a backup table of the `Sales` table with only records where the sale amount is greater than 500. | `SELECT * INTO SalesBackup FROM Sales WHERE SaleAmount > 500;` |
| **Querying & Data Retrieval** | Retrieve all product names and their prices from the `Products` table. | `SELECT ProductName, Price FROM Products;` |
| | Retrieve the distinct product categories from the `Products` table. | `SELECT DISTINCT Category FROM Products;` |
| | Retrieve all products where the price is greater than 50. | `SELECT * FROM Products WHERE Price > 50;` |
| | Retrieve all sales records sorted by sale date in descending order. | `SELECT * FROM Sales ORDER BY SaleDate DESC;` |
| | Retrieve the top 5 most expensive products. | `SELECT TOP 5 * FROM Products ORDER BY Price DESC;` |
| | Retrieve all products where the category is in ('Electronics', 'Clothing', 'Sports'). | `SELECT * FROM Products WHERE Category IN ('Electronics', 'Clothing', 'Sports');` |
| | Retrieve all sales where the sale amount is between 100 and 500. | `SELECT * FROM Sales WHERE SaleAmount BETWEEN 100 AND 500;` |
| | Retrieve all product names that start with the letter 'S'. | `SELECT ProductName FROM Products WHERE ProductName LIKE 'S%';` |
| | Retrieve all product names that contain 'phone' anywhere in the name. | `SELECT ProductName FROM Products WHERE ProductName LIKE '%phone%';` |
| **Conditional Queries** | Retrieve all products where the price is between 20 and 100 and the category is 'Electronics'. | `SELECT * FROM Products WHERE Price BETWEEN 20 AND 100 AND Category = 'Electronics';` |
| | Retrieve all products where the category is either 'Electronics' or 'Clothing'. | `SELECT * FROM Products WHERE Category = 'Electronics' OR Category = 'Clothing';` |
| | Retrieve all products that are not in the 'Clothing' category. | `SELECT * FROM Products WHERE Category <> 'Clothing';` |
| **Aggregations and Grouping** | Find the total sales amount from the `Sales` table. | `SELECT SUM(SaleAmount) AS TotalSales FROM Sales;` |
| | Retrieve the minimum and maximum product prices. | `SELECT MIN(Price) AS MinPrice, MAX(Price) AS MaxPrice FROM Products;` |
| | Count the total number of products in the `Products` table. | `SELECT COUNT(*) AS TotalProducts FROM Products;` |
| | Calculate the total revenue from the `Sales` table. | `SELECT SUM(SaleAmount) AS TotalRevenue FROM Sales;` |
| | Find the average price of all products. | `SELECT AVG(Price) AS AveragePrice FROM Products;` |
| | Group all products by category and count how many products exist in each category. | `SELECT Category, COUNT(*) AS ProductCount FROM Products GROUP BY Category;` |
| | Retrieve product categories having more than 5 products. | `SELECT Category FROM Products GROUP BY Category HAVING COUNT(*) > 5;` |
| **Data Manipulation** | Update the price of the product 'Smartphone' to 350. | `UPDATE Products SET Price = 350 WHERE ProductName = 'Smartphone';` |
| | Delete all products where the price is below 10. | `DELETE FROM Products WHERE Price < 10;` |
| | Retrieve all customers where the `phone_number` is NULL. | `SELECT * FROM Customers WHERE phone_number IS NULL;` |
| | Retrieve all products and replace any NULL price values with 0. | `SELECT ProductName, ISNULL(Price, 0) AS Price FROM Products;` |
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
| | Create a clustered index on the `ProductID` column in the `Products` table. | `CREATE

 CLUSTERED INDEX idx_ProductID ON Products (ProductID);` |
| | Create a non-clustered index on the `ProductName` column. | `CREATE NONCLUSTERED INDEX idx_ProductName ON Products (ProductName);` |
| **Keys & Constraints** | Ensure that the `ProductCode` column in the `Products` table is unique. | `ALTER TABLE Products ADD CONSTRAINT UQ_ProductCode UNIQUE (ProductCode);` |
| | Add a primary key on the `ProductID` column in the `Products` table. | `ALTER TABLE Products ADD CONSTRAINT PK_ProductID PRIMARY KEY (ProductID);` |
| | Create a foreign key in the `Sales` table that references the `ProductID` in the `Products` table. | `ALTER TABLE Sales ADD CONSTRAINT FK_Product FOREIGN KEY (ProductID) REFERENCES Products(ProductID);` |
| | Create a composite key on the `ProductID` and `OrderID` columns in the `OrderDetails` table. | `ALTER TABLE OrderDetails ADD CONSTRAINT PK_ProductOrder PRIMARY KEY (ProductID, OrderID);` |
| | Define an alternate key on the `ProductCode` column in the `Products` table. | `ALTER TABLE Products ADD CONSTRAINT AK_ProductCode UNIQUE (ProductCode);` |
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
