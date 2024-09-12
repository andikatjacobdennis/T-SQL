# T-SQL Practice and Starter Database

Welcome to the T-SQL Practice repository! This repository contains SQL scripts and exercises designed to help you practice and master T-SQL queries. It includes a starter database with sample tables and data to get you started with various SQL concepts.

## Repository Structure

- **`sql_scripts/`**: Contains SQL scripts for creating and populating the starter database, views, stored procedures, and other advanced elements.
  - **`create_and_populate_database.sql`**: SQL script to create the `SalesDB` database and populate it with sample data.
  - **`create_views_and_procedures.sql`**: SQL script for creating views, stored procedures, and additional database elements.
- **`SQL_Starter_Database_Setup.md`**: Markdown file with instructions and SQL scripts for setting up the starter database.

## Getting Started

To get started, you can use the provided SQL scripts to set up a sample database and tables on your local SQL Server or any SQL-compatible database platform.

### 1. Set Up the Database

Run the `create_and_populate_database.sql` script to create the database `SalesDB` and populate it with sample data. This will set up the following tables:
- `Products`
- `Sales`
- `Customers`

### 2. Create Views and Procedures

After setting up the database, run the `create_views_and_procedures.sql` script to create sample views and stored procedures that you can use for practice.

### 3. Practice T-SQL Queries

Refer to the markdown files for various practice queries and exercises. These exercises cover a wide range of T-SQL concepts, including:
- Basic SQL queries
- Joins and subqueries
- Aggregations and groupings
- Indexes, constraints, and triggers
- Stored procedures and functions

## Example Practice Queries

Here are a few examples of the types of queries you can practice with the provided setup:

```sql
-- Retrieve all product names and their prices
SELECT ProductName, Price FROM Products;

-- Find the total sales amount
SELECT SUM(SaleAmount) AS TotalSales FROM Sales;

-- Update the price of a product
UPDATE Products SET Price = 349.99 WHERE ProductName = 'Smartphone';

-- Create a view showing total sales by product
CREATE VIEW ProductSalesView AS
SELECT ProductName, SUM(SaleAmount) AS TotalSales
FROM Products
LEFT JOIN Sales ON Products.ProductID = Sales.ProductID
GROUP BY ProductName;
