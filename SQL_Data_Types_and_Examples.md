### SQL Data Types

SQL offers various data types to store different kinds of data. These data types are grouped into several categories, each suited for a specific kind of information. Let’s break them down and apply them to **Product** and **Sales** examples.

### 1. **Numeric Data Types**
Used to store numbers, such as prices, quantities, and discount rates.

- **INT**: Stores whole numbers. Suitable for counting items like product stock.
- **DECIMAL / NUMERIC**: Stores fixed-point numbers with precision. Used for currency or sales amounts where accuracy is important.
- **FLOAT / REAL**: Stores approximate floating-point numbers. Often avoided for financial calculations due to precision issues.

**Examples:**
```sql
-- Creating a Products table with numeric data types
CREATE TABLE Products (
    ProductID INT PRIMARY KEY,
    ProductName NVARCHAR(100),
    QuantityInStock INT, -- Storing quantity of items in stock
    Price DECIMAL(10, 2) -- Storing price with two decimal places
);

-- Inserting data
INSERT INTO Products (ProductID, ProductName, QuantityInStock, Price)
VALUES (1, 'Laptop', 100, 999.99);
```

```sql
-- Creating a Sales table with numeric data types
CREATE TABLE Sales (
    SaleID INT PRIMARY KEY,
    ProductID INT,
    QuantitySold INT, -- Storing how many items were sold
    SaleAmount DECIMAL(10, 2) -- Storing the total sale amount
);

-- Inserting data
INSERT INTO Sales (SaleID, ProductID, QuantitySold, SaleAmount)
VALUES (1, 1, 2, 1999.98);
```

---

### 2. **String Data Types**
Used to store textual data such as product names, descriptions, and customer feedback.

- **CHAR / NCHAR**: Fixed-length character data.
- **VARCHAR / NVARCHAR**: Variable-length character data. **NVARCHAR** supports Unicode, ideal for multilingual text.
  
**Examples:**
```sql
-- Storing product name and description
CREATE TABLE Products (
    ProductID INT PRIMARY KEY,
    ProductName NVARCHAR(100), -- Variable-length product name
    Description NVARCHAR(MAX) -- Product description
);

-- Inserting data
INSERT INTO Products (ProductID, ProductName, Description)
VALUES (2, 'Smartphone', 'A high-end smartphone with a 6.5-inch display.');
```

```sql
-- Storing customer feedback
CREATE TABLE CustomerFeedback (
    FeedbackID INT PRIMARY KEY,
    CustomerName NVARCHAR(100),
    Feedback NVARCHAR(MAX)
);

-- Inserting data
INSERT INTO CustomerFeedback (FeedbackID, CustomerName, Feedback)
VALUES (1, 'John Doe', 'Excellent product! Very satisfied with the purchase.');
```

---

### 3. **Date and Time Data Types**
Used for storing dates and times, such as sales dates or product release dates.

- **DATE**: Stores date only.
- **DATETIME**: Stores both date and time.
- **TIME**: Stores time of day.

**Examples:**
```sql
-- Adding product release date
CREATE TABLE Products (
    ProductID INT PRIMARY KEY,
    ProductName NVARCHAR(100),
    ReleaseDate DATE -- Storing product release date
);

-- Inserting data
INSERT INTO Products (ProductID, ProductName, ReleaseDate)
VALUES (3, 'Tablet', '2024-09-10');
```

```sql
-- Storing sale date and time
CREATE TABLE Sales (
    SaleID INT PRIMARY KEY,
    ProductID INT,
    SaleDate DATETIME -- Storing sale date and time
);

-- Inserting data
INSERT INTO Sales (SaleID, ProductID, SaleDate)
VALUES (2, 1, '2024-09-12 14:35:00');
```

---

### 4. **Binary Data Types**
Used to store binary data such as images or files.

- **BINARY**: Fixed-length binary data.
- **VARBINARY**: Variable-length binary data. Often used for storing images or files.

**Examples:**
```sql
-- Storing product images in binary format
CREATE TABLE ProductImages (
    ProductID INT PRIMARY KEY,
    ProductImage VARBINARY(MAX) -- Variable-length binary data for storing images
);

-- Inserting image (image data needs to be inserted in binary format)
INSERT INTO ProductImages (ProductID, ProductImage)
VALUES (1, 0xFFD8FFE000104A46494600010101006000600000FFD9); -- Sample binary image data
```

---

### 5. **Bit Data Type**
Used to store Boolean data (0 or 1, false or true).

**Examples:**
```sql
-- Adding a column to track whether a product is active
CREATE TABLE Products (
    ProductID INT PRIMARY KEY,
    ProductName NVARCHAR(100),
    IsActive BIT -- Storing product status (1 for active, 0 for inactive)
);

-- Inserting data
INSERT INTO Products (ProductID, ProductName, IsActive)
VALUES (4, 'Headphones', 1); -- Product is active
```

---

### 6. **Unique Identifier (GUID)**
A globally unique identifier used to uniquely identify rows across tables, useful in distributed systems.

**Examples:**
```sql
-- Using a GUID for unique identification
CREATE TABLE Sales (
    SaleID UNIQUEIDENTIFIER DEFAULT NEWID(), -- Generates a unique identifier for each sale
    ProductID INT,
    SaleDate DATETIME
);

-- Inserting data
INSERT INTO Sales (ProductID, SaleDate)
VALUES (1, '2024-09-13');
```

---

### 7. **XML Data Type**
Used to store XML data in a table.

**Examples:**
```sql
-- Storing product specifications in XML format
CREATE TABLE Products (
    ProductID INT PRIMARY KEY,
    ProductName NVARCHAR(100),
    ProductSpecs XML -- Storing specifications in XML format
);

-- Inserting data
INSERT INTO Products (ProductID, ProductName, ProductSpecs)
VALUES (5, 'Gaming PC', '<Specs><RAM>16GB</RAM><Storage>1TB</Storage></Specs>');
```
