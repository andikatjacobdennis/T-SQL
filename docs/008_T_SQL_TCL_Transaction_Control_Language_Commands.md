# 008. T-SQL TCL (Transaction Control Language) Commands

TCL (Transaction Control Language) commands manage transactions in SQL Server, ensuring data integrity by controlling how changes are committed or rolled back.

## 1. Transaction Fundamentals

### BEGIN TRANSACTION

```sql
-- Explicit transaction start
BEGIN TRANSACTION;
-- or
BEGIN TRAN;
-- or with named transaction
BEGIN TRANSACTION UpdateInventory;
```

### COMMIT TRANSACTION

```sql
-- Permanently save changes
COMMIT TRANSACTION;
-- or
COMMIT;
-- or for named transaction
COMMIT TRANSACTION UpdateInventory;
```

### ROLLBACK TRANSACTION

```sql
-- Undo all changes in transaction
ROLLBACK TRANSACTION;
-- or
ROLLBACK;
-- or to savepoint
ROLLBACK TRANSACTION TO SavepointName;
```

## 2. Savepoints

### Creating Savepoints

```sql
BEGIN TRANSACTION;

-- Initial operation
UPDATE Products SET Stock = Stock - 10 WHERE ProductID = 5;

-- Create savepoint
SAVE TRANSACTION BeforeSecondUpdate;

-- Risky operation
UPDATE Orders SET Status = 'Shipped' WHERE OrderID = 1001;

-- Conditionally rollback to savepoint
IF @@ERROR <> 0
    ROLLBACK TRANSACTION BeforeSecondUpdate;

COMMIT TRANSACTION;
```

## 3. Transaction Isolation Levels

### Setting Isolation Levels

```sql
-- Read uncommitted (dirty reads allowed)
SET TRANSACTION ISOLATION LEVEL READ UNCOMMITTED;
BEGIN TRANSACTION;
-- Operations...
COMMIT;

-- Read committed (default)
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;

-- Repeatable read
SET TRANSACTION ISOLATION LEVEL REPEATABLE READ;

-- Serializable (highest isolation)
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;

-- Snapshot (versioning)
ALTER DATABASE OrderDB SET ALLOW_SNAPSHOT_ISOLATION ON;
SET TRANSACTION ISOLATION LEVEL SNAPSHOT;
```

## 4. Nested Transactions

```sql
BEGIN TRANSACTION OuterTran;  -- @@TRANCOUNT = 1

    -- First operation
    INSERT INTO AuditLog (Action) VALUES ('Started process');

    BEGIN TRANSACTION InnerTran;  -- @@TRANCOUNT = 2
        UPDATE Accounts SET Balance = Balance - 100 WHERE AccountID = 1;
        UPDATE Accounts SET Balance = Balance + 100 WHERE AccountID = 2;

        -- Only commits inner transaction
        COMMIT TRANSACTION InnerTran;  -- @@TRANCOUNT = 1

    -- More operations
    INSERT INTO AuditLog (Action) VALUES ('Completed transfers');

    -- Must commit outer transaction too
    COMMIT TRANSACTION OuterTran;  -- @@TRANCOUNT = 0
```

## 5. Distributed Transactions

```sql
-- Start distributed transaction
BEGIN DISTRIBUTED TRANSACTION;

-- Operation on local server
UPDATE OrderDB.dbo.Orders SET Status = 'Processed' WHERE OrderID = 1001;

-- Operation on linked server
EXEC LinkedServer.InventoryDB.dbo.UpdateStock @ProductID = 5, @Qty = -1;

-- Commit or rollback
IF @@ERROR = 0
    COMMIT TRANSACTION;
ELSE
    ROLLBACK TRANSACTION;
```

## 6. Transaction Best Practices

### Error Handling with TRY/CATCH

```sql
BEGIN TRY
    BEGIN TRANSACTION;

    -- Critical operations
    UPDATE Products SET Stock = Stock - 1 WHERE ProductID = 5;
    INSERT INTO OrderDetails (OrderID, ProductID) VALUES (1001, 5);

    COMMIT TRANSACTION;
END TRY
BEGIN CATCH
    IF @@TRANCOUNT > 0
        ROLLBACK TRANSACTION;

    -- Log error
    INSERT INTO ErrorLog (ErrorMsg, ErrorTime)
    VALUES (ERROR_MESSAGE(), GETDATE());

    THROW;  -- Re-throw error to client
END CATCH
```

### Transaction Duration Guidelines

- Keep transactions as short as possible
- Avoid user interaction within transactions
- Process large datasets in batches

### Monitoring Active Transactions

```sql
-- View open transactions
DBCC OPENTRAN;

-- Detailed transaction info
SELECT
    t.transaction_id,
    s.login_name,
    s.host_name,
    t.name,
    t.transaction_begin_time
FROM sys.dm_tran_active_transactions t
JOIN sys.dm_exec_sessions s ON t.transaction_id = s.open_transaction_count;
```

## 7. Complete Transaction Example

```sql
-- 1. Check environment
IF @@TRANCOUNT > 0
BEGIN
    RAISERROR('Existing transaction detected', 16, 1);
    RETURN;
END

-- 2. Set isolation level
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;

-- 3. Begin transaction
BEGIN TRANSACTION ProcessOrder;

BEGIN TRY
    -- 4. Core operations
    -- a) Reserve inventory
    UPDATE Inventory
    SET Quantity = Quantity - @OrderQty
    WHERE ProductID = @ProductID
    AND Quantity >= @OrderQty;

    IF @@ROWCOUNT = 0
    BEGIN
        RAISERROR('Insufficient inventory', 16, 1);
        ROLLBACK;
        RETURN;
    END

    -- b) Create order record
    INSERT INTO Orders (CustomerID, OrderDate, Status)
    VALUES (@CustomerID, GETDATE(), 'Processing');

    SET @OrderID = SCOPE_IDENTITY();

    -- c) Add order details
    INSERT INTO OrderDetails (OrderID, ProductID, Quantity)
    VALUES (@OrderID, @ProductID, @OrderQty);

    -- d) Create audit record
    INSERT INTO OrderAudit (OrderID, Action, ActionDate)
    VALUES (@OrderID, 'Created', GETDATE());

    -- 5. Commit if successful
    COMMIT TRANSACTION ProcessOrder;

    -- 6. Return success
    SELECT @OrderID AS NewOrderID, 'Success' AS Result;
END TRY
BEGIN CATCH
    -- 7. Rollback on error
    IF @@TRANCOUNT > 0
        ROLLBACK TRANSACTION ProcessOrder;

    -- 8. Log error details
    INSERT INTO ErrorLog (ErrorNumber, ErrorSeverity, ErrorMessage)
    VALUES (ERROR_NUMBER(), ERROR_SEVERITY(), ERROR_MESSAGE());

    -- 9. Return failure
    SELECT NULL AS NewOrderID, 'Failed: ' + ERROR_MESSAGE() AS Result;
END CATCH
```

## Key TCL Concepts

### ACID Properties

- Atomicity: All operations succeed or fail together
- Consistency: Database remains in valid state
- Isolation: Concurrent transactions don't interfere
- Durability: Committed changes survive failures

### Transaction States

- Active: Executing operations
- Partially Committed: After final operation
- Committed: After successful completion
- Failed: After unsuccessful operations
- Aborted: After rollback

### Locking Behavior

- Transactions acquire locks automatically
- Higher isolation levels = more restrictive locking
- Long transactions = potential blocking issues
