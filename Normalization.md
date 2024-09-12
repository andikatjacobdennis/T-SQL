## Normalization

Normalization is a database design process that organizes tables to reduce data redundancy and improve data integrity. The goal of normalization is to divide large tables into smaller, related tables and define relationships between them to ensure that data is stored efficiently and accurately.

### **Types of Normal Forms**

1. **First Normal Form (1NF)**
2. **Second Normal Form (2NF)**
3. **Third Normal Form (3NF)**
4. **Boyce-Codd Normal Form (BCNF)**
5. **Fourth Normal Form (4NF)**
6. **Fifth Normal Form (5NF)**

### **Normalization Examples with Product and Sales Data**

#### **1. First Normal Form (1NF)**
A table is in 1NF if it contains only atomic (indivisible) values and each column contains values of a single type.

**Example Table (Before 1NF):**
```
Products
ProductID | ProductName | Categories          | Price
1         | Laptop      | Electronics, Computers| 899.99
2         | Smartphone  | Electronics, Mobile   | 299.99
3         | T-Shirt     | Clothing              | 19.99
```

**Issues:**
- The `Categories` column contains multiple values.

**Table (After 1NF):**
```
Products
ProductID | ProductName | Price
1         | Laptop      | 899.99
2         | Smartphone  | 299.99
3         | T-Shirt     | 19.99

ProductCategories
ProductID | Category
1         | Electronics
1         | Computers
2         | Electronics
2         | Mobile
3         | Clothing
```

#### **2. Second Normal Form (2NF)**
A table is in 2NF if it is in 1NF and all non-key attributes are fully functionally dependent on the entire primary key.

**Example Table (Before 2NF):**
```
Sales
SaleID | ProductID | ProductName | SaleAmount | SaleDate
1      | 1         | Laptop      | 899.99      | 2024-09-01
2      | 2         | Smartphone  | 299.99      | 2024-09-02
3      | 1         | Laptop      | 899.99      | 2024-09-04
```

**Issues:**
- `ProductName` depends only on `ProductID`, not on the full primary key (`SaleID`, `ProductID`).

**Table (After 2NF):**
```
Sales
SaleID | ProductID | SaleAmount | SaleDate
1      | 1         | 899.99      | 2024-09-01
2      | 2         | 299.99      | 2024-09-02
3      | 1         | 899.99      | 2024-09-04

Products
ProductID | ProductName | Price
1         | Laptop      | 899.99
2         | Smartphone  | 299.99
```

#### **3. Third Normal Form (3NF)**
A table is in 3NF if it is in 2NF and all the attributes are functionally dependent only on the primary key.

**Example Table (Before 3NF):**
```
Sales
SaleID | ProductID | SaleAmount | SaleDate | ProductPrice
1      | 1         | 899.99      | 2024-09-01 | 899.99
2      | 2         | 299.99      | 2024-09-02 | 299.99
3      | 1         | 899.99      | 2024-09-04 | 899.99
```

**Issues:**
- `ProductPrice` is dependent on `ProductID`, which is a transitive dependency.

**Table (After 3NF):**
```
Sales
SaleID | ProductID | SaleAmount | SaleDate
1      | 1         | 899.99      | 2024-09-01
2      | 2         | 299.99      | 2024-09-02
3      | 1         | 899.99      | 2024-09-04

Products
ProductID | ProductName | Price
1         | Laptop      | 899.99
2         | Smartphone  | 299.99
```

#### **4. Boyce-Codd Normal Form (BCNF)**
A table is in BCNF if it is in 3NF and for every one of its non-trivial functional dependencies, X → Y, X is a superkey.

**Example Table (Before BCNF):**
```
ProductSales
ProductID | SaleDate | SalesPerson
1         | 2024-09-01 | John
1         | 2024-09-02 | Jane
```

**Issues:**
- `SalesPerson` depends on `ProductID` and `SaleDate`, but `ProductID` and `SaleDate` together are not necessarily a superkey.

**Table (After BCNF):**
```
ProductSales
ProductID | SaleDate | SalesPerson
1         | 2024-09-01 | John
1         | 2024-09-02 | Jane

SalesPersons
SalesPersonID | SalesPersonName
1             | John
2             | Jane
```

### **Summary**
Normalization involves decomposing tables to eliminate redundancy and ensure that each table represents a single entity or concept. The process is carried out through various normal forms, each addressing specific types of redundancy and ensuring data integrity.

- **1NF** ensures atomicity of data.
- **2NF** removes partial dependencies.
- **3NF** eliminates transitive dependencies.
- **BCNF** resolves anomalies that are not handled by 3NF.

By applying these normalization rules, you ensure that the database structure is optimized for data integrity and efficiency.
