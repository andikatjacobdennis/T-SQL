## ACID

ACID is a set of properties that guarantee database transactions are processed reliably. ACID stands for Atomicity, Consistency, Isolation, and Durability. Let's break down each property with an example involving the `Products` and `Sales` tables:

### Atomicity

**Atomicity** ensures that all parts of a transaction are completed successfully, or none of them are applied. It’s an "all-or-nothing" approach.

**Example:**

Imagine we want to insert a new sale and update the stock quantity for a product. If the operation fails, neither the sale should be recorded nor the stock quantity updated. Here’s how you can handle it in T-SQL:

```sql
BEGIN TRANSACTION;

BEGIN TRY
    -- Insert a new sale
    INSERT INTO Sales (ProductID, SaleAmount, SaleDate)
    VALUES (1, 100, GETDATE());
    
    -- Update the stock quantity for the product
    UPDATE Products
    SET StockQuantity = StockQuantity - 1
    WHERE ProductID = 1;

    -- Commit the transaction if both operations succeed
    COMMIT TRANSACTION;
END TRY
BEGIN CATCH
    -- Rollback the transaction if any operation fails
    ROLLBACK TRANSACTION;
    -- Optional: Handle the error
    PRINT 'Transaction failed. Rolling back.';
END CATCH;
```

### Consistency

**Consistency** ensures that a transaction brings the database from one valid state to another. After a transaction, the database should remain in a consistent state.

**Example:**

Suppose we have a constraint that the `SaleAmount` in the `Sales` table cannot be negative, and the `StockQuantity` in the `Products` table should not go below zero.

```sql
-- Create constraints
ALTER TABLE Sales
ADD CONSTRAINT CK_SaleAmount_Positive CHECK (SaleAmount >= 0);

ALTER TABLE Products
ADD CONSTRAINT CK_StockQuantity_NonNegative CHECK (StockQuantity >= 0);
```

With these constraints, if a transaction tries to insert a negative sale amount or update the stock quantity to a negative value, it will fail, thus preserving the database's consistency.

### Isolation

**Isolation** ensures that transactions are executed in isolation from each other. Changes made by one transaction are not visible to other transactions until they are committed.

**Example:**

Imagine two transactions are running simultaneously. One transaction is updating the `StockQuantity` for a product, while another is trying to read the same value. Isolation ensures that each transaction does not interfere with the other.

```sql
-- Transaction 1
BEGIN TRANSACTION;
UPDATE Products
SET StockQuantity = StockQuantity - 5
WHERE ProductID = 1;
-- Transaction 2 (running at the same time)
BEGIN TRANSACTION;
SELECT StockQuantity FROM Products WHERE ProductID = 1;
-- If Transaction 1 commits, Transaction 2 should see the updated value

COMMIT TRANSACTION;  -- For both transactions
```

In this example, Transaction 2 will only see the updated stock quantity if Transaction 1 commits before Transaction 2 finishes.

### Durability

**Durability** ensures that once a transaction is committed, its changes are permanent, even in the event of a system failure.

**Example:**

After a transaction is committed, the changes are written to the database, and recovery mechanisms ensure that these changes are preserved even if the system crashes immediately afterward.

```sql
BEGIN TRANSACTION;

-- Insert a sale
INSERT INTO Sales (ProductID, SaleAmount, SaleDate)
VALUES (2, 150, GETDATE());

-- Commit the transaction
COMMIT TRANSACTION;

-- The sale should be saved permanently, even if a system crash occurs right after.
```
