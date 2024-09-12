### **Database Creation & Management**

1. **SQL - Create Database**  
   *Practice*:  
   Create a new database called `SalesDB`.

2. **SQL - Select Database**  
   *Practice*:  
   Select and use the `SalesDB` database.

3. **SQL - Show Databases**  
   *Practice*:  
   List all available databases on the server.

4. **SQL - Rename Database**  
   *Practice*:  
   Rename `OldSalesDB` to `NewSalesDB`.

5. **SQL - Backup Database**  
   *Practice*:  
   Backup the `SalesDB` database.

6. **SQL - Drop Database**  
   *Practice*:  
   Drop the database `TestDB`.

---

### **Table Creation & Management**

7. **SQL - Create Table**  
   *Practice*:  
   Create a table `Products` with columns `ProductID`, `ProductName`, `Price`, and `Category`.

8. **SQL - Show Tables**  
   *Practice*:  
   Retrieve all tables from the `SalesDB` database.

9. **SQL - Alter Tables**  
   *Practice*:  
   Add a new column `StockQuantity` to the `Products` table.

10. **SQL - Rename Table**  
    *Practice*:  
    Rename the table `OldProducts` to `NewProducts`.

11. **SQL - Clone Tables**  
    *Practice*:  
    Create a clone of the `Products` table including the schema and data.

12. **SQL - Temporary Tables**  
    *Practice*:  
    Create a temporary table for storing product sales during a session.

13. **SQL - Constraints**  
    *Practice*:  
    Add a foreign key constraint to the `Sales` table referencing `Products`.

14. **SQL - Truncate Table**  
    *Practice*:  
    Truncate all records from the `Sales` table.

15. **SQL - Delete Table**  
    *Practice*:  
    Permanently delete the `OldProducts` table.

16. **SQL - Drop Table**  
    *Practice*:  
    Drop the `TemporarySales` table.

---

### **Inserting Data into Tables**

17. **SQL Insert Into**  
    *Practice*:  
    Insert a new product into the `Products` table with name 'Smartphone' and price 299.

18. **SQL Insert Into Select**  
    *Practice*:  
    Insert all records from the `Products` table into a new table called `BackupProducts`.

19. **SQL Select Into**  
    *Practice*:  
    Create a backup table of the `Sales` table with only records where the sale amount is greater than 500.

---

### **Querying & Data Retrieval**

20. **SQL Select**  
    *Practice*:  
    Retrieve all product names and their prices from the `Products` table.

21. **SQL Select Distinct**  
    *Practice*:  
    Retrieve the distinct product categories from the `Products` table.

22. **SQL Where**  
    *Practice*:  
    Retrieve all products where the price is greater than 50.

23. **SQL Order By**  
    *Practice*:  
    Retrieve all sales records sorted by sale date in descending order.

24. **SQL Select Top**  
    *Practice*:  
    Retrieve the top 5 most expensive products.

25. **SQL In**  
    *Practice*:  
    Retrieve all products where the category is in ('Electronics', 'Clothing', 'Sports').

26. **SQL Between**  
    *Practice*:  
    Retrieve all sales where the sale amount is between 100 and 500.

27. **SQL Like**  
    *Practice*:  
    Retrieve all product names that start with the letter 'S'.

28. **SQL Wildcards**  
    *Practice*:  
    Retrieve all product names that contain 'phone' anywhere in the name.

---

### **Conditional Queries**

29. **SQL And**  
    *Practice*:  
    Retrieve all products where the price is between 20 and 100 and the category is 'Electronics'.

30. **SQL Or**  
    *Practice*:  
    Retrieve all products where the category is either 'Electronics' or 'Clothing'.

31. **SQL Not**  
    *Practice*:  
    Retrieve all products that are not in the 'Clothing' category.

---

### **Aggregations and Grouping**

32. **SQL Aggregate Functions**  
    *Practice*:  
    Find the total sales amount from the `Sales` table.

33. **SQL Min and Max**  
    *Practice*:  
    Retrieve the minimum and maximum product prices.

34. **SQL Count**  
    *Practice*:  
    Count the total number of products in the `Products` table.

35. **SQL Sum**  
    *Practice*:  
    Calculate the total revenue from the `Sales` table.

36. **SQL Avg**  
    *Practice*:  
    Find the average price of all products.

37. **SQL Group By**  
    *Practice*:  
    Group all products by category and count how many products exist in each category.

38. **SQL Having**  
    *Practice*:  
    Retrieve product categories having more than 5 products.

---

### **Data Manipulation**

39. **SQL Update**  
    *Practice*:  
    Update the price of the product 'Smartphone' to 350.

40. **SQL Delete**  
    *Practice*:  
    Delete all products where the price is below 10.

41. **SQL Null Values**  
    *Practice*:  
    Retrieve all customers where the `phone_number` is NULL.

42. **SQL Null Functions**  
    *Practice*:  
    Retrieve all products and replace any NULL price values with 0.

---

### **Joins & Set Operations**

43. **SQL Joins**  
    *Practice*:  
    Retrieve all sales with the corresponding product name by joining `Sales` and `Products` tables.

44. **SQL Inner Join**  
    *Practice*:  
    Retrieve the customer name and the corresponding sales amount by joining `Customers` and `Sales` tables.

45. **SQL Left Join**  
    *Practice*:  
    Retrieve all products and their sales data, showing NULL for products that haven’t been sold.

46. **SQL Right Join**  
    *Practice*:  
    Retrieve all sales and the product details, showing NULL for products that no longer exist.

47. **SQL Full Join**  
    *Practice*:  
    Retrieve all products and their sales information, even if there is no match on either side.

48. **SQL Self Join**  
    *Practice*:  
    Retrieve all products that have the same price by joining the `Products` table to itself.

49. **SQL Union**  
    *Practice*:  
    Retrieve all distinct product names from `Products` and `Sales` tables.

---

### **Subqueries and Advanced Queries**

50. **SQL Exists**  
    *Practice*:  
    Retrieve all customers who have made a purchase.

51. **SQL Any, All**  
    *Practice*:  
    Retrieve all products where the price is greater than all products in the 'Clothing' category.

52. **SQL Case**  
    *Practice*:  
    Retrieve all products and add a new column showing 'Expensive' if the price is above 100, otherwise 'Cheap'.

---

### **Indexes**

53. **SQL Indexes**  
    *Practice*:  
    Create an index on the `ProductName` column for faster searches.

54. **SQL Create Index**  
    *Practice*:  
    Create an index on the `SaleDate` column in the `Sales` table.

55. **SQL Drop Index**  
    *Practice*:  
    Drop the index on the `ProductName` column.

56. **SQL Show Indexes**  
    *Practice*:  
    Retrieve all indexes on the `Products` table.

57. **SQL Unique Index**  
    *Practice*:  
    Create a unique index on the `ProductCode` column in the `Products` table.

58. **SQL Clustered Index**  
    *Practice*:  
    Create a clustered index on the `ProductID` column in the `Products` table.

59. **SQL Non-Clustered Index**  
    *Practice*:  
    Create a non-clustered index on the `ProductName` column.

---

### **Keys & Constraints**

60. **SQL Unique Key**  
    *Practice*:  
    Ensure that the `ProductCode` column in the `Products` table is unique.

61. **SQL Primary Key**  
    *Practice*:  
    Add a primary key on the `ProductID` column in the `Products` table.

62. **SQL Foreign Key**  
    *Practice*:  
    Create a foreign key in the `Sales` table that references the `ProductID` in the `Products` table.

63. **SQL Composite Key**  
    *Practice*:  
    Create a composite key on the `ProductID` and `OrderID` columns in the `OrderDetails` table.

64. **SQL Alternate Key**  
    *Practice*:  
    Define an alternate key on the `ProductCode` column in the `Products` table.

---

### **Views**

65. **SQL Create Views**  
    *Practice*:  
    Create a view that shows product names and total sales for each product.

66. **SQL Update Views**  
    *Practice*:  
    Update the `ProductSalesView` to include the average sale amount.

67. **SQL Drop Views**  
    *Practice*:  
    Drop the `ObsoleteView` from the database.

68. **

SQL Rename Views**  
    *Practice*:  
    Rename `ProductSalesView` to `ProductRevenueView`.

---

### **Stored Procedures & Functions**

69. **SQL Stored Procedures**  
    *Practice*:  
    Create a stored procedure to add a new sale record to the `Sales` table.

70. **Functions, Cursor, Transactions**  
    *Practice*:  
    Write a function that calculates the total sales for a given product.

---

### **Advanced Concepts**

71. **Conditions, Loops**  
    *Practice*:  
    Write a loop to update prices for all products that meet a specific condition.

72. **Triggers**  
    *Practice*:  
    Create a trigger that updates the stock quantity in the `Products` table after every insert into `Sales`.

73. **Grant/Revoke**  
    *Practice*:  
    Grant a user permission to view the `Products` table but revoke their ability to delete records.
