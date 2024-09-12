### **1. Create Database and Tables**

```sql
-- Create the database
CREATE DATABASE SalesDB;
USE SalesDB;

-- Create the Products table
CREATE TABLE Products (
    ProductID INT PRIMARY KEY,
    ProductName NVARCHAR(100),
    Price DECIMAL(10, 2),
    Category NVARCHAR(50),
    StockQuantity INT
);

-- Create the Sales table
CREATE TABLE Sales (
    SaleID INT PRIMARY KEY,
    ProductID INT,
    SaleAmount DECIMAL(10, 2),
    SaleDate DATE,
    FOREIGN KEY (ProductID) REFERENCES Products(ProductID)
);

-- Create the Customers table
CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    CustomerName NVARCHAR(100),
    PhoneNumber NVARCHAR(20)
);
```

### **2. Insert Sample Data**

```sql
-- Insert data into Products
INSERT INTO Products (ProductID, ProductName, Price, Category, StockQuantity)
VALUES
(1, 'Smartphone', 299.99, 'Electronics', 50),
(2, 'Laptop', 899.99, 'Electronics', 30),
(3, 'T-Shirt', 19.99, 'Clothing', 100),
(4, 'Coffee Maker', 49.99, 'Home Appliances', 20);

-- Insert data into Sales
INSERT INTO Sales (SaleID, ProductID, SaleAmount, SaleDate)
VALUES
(1, 1, 299.99, '2024-09-01'),
(2, 2, 899.99, '2024-09-02'),
(3, 3, 19.99, '2024-09-03'),
(4, 1, 299.99, '2024-09-04'),
(5, 4, 49.99, '2024-09-05');

-- Insert data into Customers
INSERT INTO Customers (CustomerID, CustomerName, PhoneNumber)
VALUES
(1, 'John Doe', '555-1234'),
(2, 'Jane Smith', '555-5678'),
(3, 'Mike Johnson', '555-8765');
```

### **3. Create Sample Views**

```sql
-- Create a view for product sales
CREATE VIEW ProductSalesView AS
SELECT Products.ProductName, SUM(Sales.SaleAmount) AS TotalSales
FROM Products
LEFT JOIN Sales ON Products.ProductID = Sales.ProductID
GROUP BY Products.ProductName;
```

### **4. Stored Procedures and Functions**

```sql
-- Create a stored procedure to add a new sale
CREATE PROCEDURE AddSale 
    @ProductID INT, 
    @SaleAmount DECIMAL(10, 2), 
    @SaleDate DATE 
AS 
BEGIN 
    INSERT INTO Sales (ProductID, SaleAmount, SaleDate) 
    VALUES (@ProductID, @SaleAmount, @SaleDate); 
END;

-- Create a function to calculate total sales for a product
CREATE FUNCTION TotalSalesForProduct (@ProductID INT)
RETURNS DECIMAL(10, 2)
AS
BEGIN
    RETURN (SELECT ISNULL(SUM(SaleAmount), 0) FROM Sales WHERE ProductID = @ProductID);
END;
```

### **5. Indexes**

```sql
-- Create an index on ProductName
CREATE INDEX idx_ProductName ON Products (ProductName);

-- Create a unique index on ProductID
CREATE UNIQUE INDEX idx_ProductID ON Products (ProductID);

-- Create a clustered index on ProductID
CREATE CLUSTERED INDEX idx_ProductID_Clustered ON Products (ProductID);
```

### **6. Constraints and Foreign Keys**

```sql
-- Add a unique constraint on ProductName
ALTER TABLE Products ADD CONSTRAINT UQ_ProductName UNIQUE (ProductName);

-- Add a foreign key constraint to Sales table
ALTER TABLE Sales ADD CONSTRAINT FK_Product FOREIGN KEY (ProductID) REFERENCES Products(ProductID);
```

### **7. Triggers**

```sql
-- Create a trigger to update stock quantity after a sale
CREATE TRIGGER UpdateStock
ON Sales
AFTER INSERT
AS
BEGIN
    UPDATE Products
    SET StockQuantity = StockQuantity - 1
    WHERE ProductID IN (SELECT ProductID FROM inserted);
END;
```

### **8. Views (Update View)**

```sql
-- Update the view to include average sales
CREATE OR ALTER VIEW ProductSalesView AS
SELECT Products.ProductName, 
       SUM(Sales.SaleAmount) AS TotalSales, 
       AVG(Sales.SaleAmount) AS AverageSales
FROM Products
LEFT JOIN Sales ON Products.ProductID = Sales.ProductID
GROUP BY Products.ProductName;
```

### **9. Grant and Revoke Permissions**

```sql
-- Grant SELECT permission on Products table
GRANT SELECT ON Products TO [username];

-- Revoke DELETE permission from Products table
REVOKE DELETE ON Products FROM [username];
```

### **10. Temporary Tables**

```sql
-- Create a temporary table for sales analysis
CREATE TABLE #TempSales (
    SaleID INT,
    ProductID INT,
    SaleAmount DECIMAL(10, 2)
);

-- Insert data into the temporary table
INSERT INTO #TempSales (SaleID, ProductID, SaleAmount)
VALUES (6, 2, 899.99);

-- Drop the temporary table
DROP TABLE #TempSales;
```
