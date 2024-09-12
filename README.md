# T-SQL Practice Repository

Welcome to the T-SQL Practice Repository! This repository offers resources for practicing T-SQL queries, including a starter database setup and a collection of exercises covering various SQL topics.

## Repository Structure

1. **SQL_Starter_Database_Setup.md**: Contains instructions and SQL scripts for creating and populating a starter database. This file guides you through setting up the initial database and tables for practice.

2. **SQL_Exercises_and_Examples.md**: A comprehensive collection of T-SQL queries and exercises. This file includes examples and practice queries ranging from basic database operations to advanced topics like indexing, constraints, and stored procedures.

## Getting Started

### 1. Set Up the Database

1. Open the `SQL_Starter_Database_Setup.md` file.
2. Follow the instructions to execute the SQL scripts provided. These scripts will create a sample database named `SalesDB` and populate it with sample tables and data.

### 2. Practice T-SQL Queries

1. Open the `SQL_Exercises_and_Examples.md` file.
2. Use the queries and exercises provided to practice various T-SQL concepts. The exercises cover:
   - Basic SQL queries
   - Joins and subqueries
   - Aggregations and groupings
   - Indexes, constraints, and triggers
   - Stored procedures and functions

## Example Queries

Here are a few example queries from the `SQL_Exercises_and_Examples.md` file to get you started:

- Retrieve all products with their prices:
  ```sql
  SELECT ProductName, Price FROM Products;
  ```

- Find total sales amount:
  ```sql
  SELECT SUM(SaleAmount) AS TotalSales FROM Sales;
  ```

- Update the price of a specific product:
  ```sql
  UPDATE Products SET Price = 349.99 WHERE ProductName = 'Smartphone';
  ```

- Create a view to show total sales by product:
  ```sql
  CREATE VIEW ProductSalesView AS
  SELECT ProductName, SUM(SaleAmount) AS TotalSales
  FROM Products
  LEFT JOIN Sales ON Products.ProductID = Sales.ProductID
  GROUP BY ProductName;
  ```

## Contributing

Contributions are welcome! If you have additional T-SQL exercises or improvements to suggest, please feel free to submit a pull request. You can also open issues for any questions or feedback.

## License

This repository is licensed under the MIT License. See the `LICENSE` file for details.

## Contact

For any questions or feedback, please open an issue or contact me directly at andikatjacobdennis@gmail.com.

Happy querying and practicing!
