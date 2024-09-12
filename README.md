# T-SQL Practice Repository

Welcome to the T-SQL Practice Repository! This repository offers resources for practicing T-SQL queries, including a starter database setup and a collection of exercises covering various SQL topics.

## Repository Structure

1. **[SQL_Starter_Database_Setup.md](SQL_Starter_Database_Setup.md)**: Contains instructions and SQL scripts for creating and populating a starter database. This file guides you through setting up the initial database and tables for practice.

2. **[SQL_Exercises_and_Examples.md](SQL_Exercises_and_Examples.md)**: A comprehensive collection of T-SQL queries and exercises. This file includes examples and practice queries ranging from basic database operations to advanced topics like indexing, constraints, and stored procedures.

3. **[ACID.md](ACID.md)**: Provides a detailed explanation of ACID properties (Atomicity, Consistency, Isolation, Durability) with T-SQL examples.

4. **[Normalization.md](Normalization.md)**: Explains database normalization, including different normal forms and practical examples.

5. **[Step-by-Step_Technique_to_Create_a_DFD.md](Step-by-Step_Technique_to_Create_a_DFD.md)**: Provides a detailed technique for creating Data Flow Diagrams (DFDs) from scratch, including defining processes, data stores, data flows, and external entities.

6. **[Step-by-Step_Technique_to_Create_an_ER_Diagram.md](Step-by-Step_Technique_to_Create_an_ER_Diagram.md)**: Offers a step-by-step guide to creating Entity-Relationship (ER) diagrams, including identifying entities, attributes, relationships, and cardinality.

## Getting Started

### 1. Set Up the Database

1. Open the [SQL_Starter_Database_Setup.md](SQL_Starter_Database_Setup.md) file.
2. Follow the instructions to execute the SQL scripts provided. These scripts will create a sample database named `SalesDB` and populate it with sample tables and data.

### 2. Practice T-SQL Queries

1. Open the [SQL_Exercises_and_Examples.md](SQL_Exercises_and_Examples.md) file.
2. Use the queries and exercises provided to practice various T-SQL concepts. The exercises cover:
   - Basic SQL queries
   - Joins and subqueries
   - Aggregations and groupings
   - Indexes, constraints, and triggers
   - Stored procedures and functions

### 3. Learn About ACID and Normalization

1. Review the [ACID.md](ACID.md) file for a detailed explanation of ACID properties and how they apply to database transactions.
2. Consult the [Normalization.md](Normalization.md) file to understand database normalization, its importance, and how to implement it.

### 4. Create Diagrams

1. Refer to the [Step-by-Step_Technique_to_Create_a_DFD.md](Step-by-Step_Technique_to_Create_a_DFD.md) for guidance on creating Data Flow Diagrams (DFDs), which will help in visualizing processes, data flows, and interactions.
2. Consult the [Step-by-Step_Technique_to_Create_an_ER_Diagram.md](Step-by-Step_Technique_to_Create_an_ER_Diagram.md) to learn how to create Entity-Relationship diagrams, focusing on defining entities, attributes, relationships, and cardinality.

## Example Queries

Here are a few example queries from the [SQL_Exercises_and_Examples.md](SQL_Exercises_and_Examples.md) file to get you started:

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

This repository is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Contact

For any questions or feedback, please open an issue or contact me directly at andikatjacobdennis@gmail.com.

Happy querying and practicing!
