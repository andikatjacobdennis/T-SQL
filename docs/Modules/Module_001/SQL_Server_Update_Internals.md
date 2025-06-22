# SQL Server UPDATE Command – Internal Workings

> **Try it live!** Run this in SSMS to see the internals in action:
>
> ```sql
> -- Setup
> CREATE TABLE Employees (EmployeeID INT PRIMARY KEY, Name NVARCHAR(100), Salary DECIMAL(10, 2));
> INSERT INTO Employees VALUES (1, 'Alice', 50000), (2, 'Bob', 60000);
>
> -- Observe this UPDATE
> UPDATE Employees SET Salary = Salary + 5000 WHERE EmployeeID = 1;
> ```

## Architecture Overview

![SQL Server Architecture](/images/sql_server_architecture.png)

### Key Components Involved:

| Component             | Role During UPDATE                      |
| --------------------- | --------------------------------------- |
| **Protocol Layer**    | Receives TDS packet from client         |
| **Relational Engine** | Parses SQL, optimizes plan              |
| **Storage Engine**    | Manages data access, locks, and logging |
| **Transaction Log**   | Records all changes (WAL protocol)      |

## Step-by-Step Execution Sequence

![UPDATE Sequence Diagram](/images/SQL_Server_UPDATE_Sequence.png)

### Phase 1: Query Processing

1. **Client Application** sends `UPDATE` via Tabular Data Stream (TDS).
2. **Parser/Algebraizer** checks syntax and converts to logical tree.
3. **Optimizer** generates execution plan (or reuses cached plan).

### Phase 2: Data Modification

4. **Storage Engine** locates row via index traversal.
5. **Lock Manager** acquires locks (`IX` for table, `U` for row).
6. **Transaction Manager** begins implicit transaction.

### Phase 3: Persistence

7. **Log Manager** writes "before/after" images to transaction log.
8. **Buffer Pool** updates the in-memory data page.
9. On commit, log records `LOP_COMMIT_XACT` and releases locks.

## Live Observation in SSMS

### Tools You'll Need:

- **SQL Server Management Studio (SSMS)**
- **System Views/DMVs** (`sys.dm_tran_locks`, `sys.dm_os_buffer_descriptors`)
- **Log Reader** (`fn_dblog()` – requires `sysadmin`)

### Step-by-Step Instructions

#### 1. Enable and View the Actual Execution Plan

```sql
-- Press Ctrl+M to enable "Include Actual Execution Plan"
UPDATE Employees SET Salary = Salary + 5000 WHERE EmployeeID = 1;
```

**What to Observe**:

- Operators like `Clustered Index Update`
- Any implicit `Key Lookup` or `Index Seek`
- Row modification strategy

#### 2. Monitor Locks in Real Time

```sql
-- Run in a second window while the first transaction is open
SELECT resource_type, request_mode, resource_description
FROM sys.dm_tran_locks
WHERE resource_database_id = DB_ID();
```

**Expected Locks**:

- `OBJECT (IX)` → Table-level intent
- `KEY (U)` or `PAGE (IU)` → Row/Page-level update locks

#### 3. Track Data Page Usage via Buffer Pool

Check if data is accessed from memory (Buffer Pool) or disk:

```sql
SELECT COUNT(*) AS page_count
FROM sys.dm_os_buffer_descriptors
WHERE database_id = DB_ID() AND page_type = 'DATA_PAGE';
```

Use this to determine if SQL Server had to load data from disk or not.

#### 4. Inspect Transaction Log (WAL in Action)

```sql
-- Run after executing UPDATE (sysadmin only)
SELECT [Current LSN], Operation, Context, AllocUnitName, [Transaction ID]
FROM fn_dblog(NULL, NULL)
WHERE Operation IN ('LOP_BEGIN_XACT', 'LOP_MODIFY_ROW', 'LOP_COMMIT_XACT')
  AND AllocUnitName LIKE '%Employees%';
```

**Look for**:

- `LOP_BEGIN_XACT`: Start of transaction
- `LOP_MODIFY_ROW`: Data modification
- `LOP_COMMIT_XACT`: Final commit and durability

#### 5. View Message Sent Back to Client

After executing the update:

> **(1 row affected)**
> This represents the successful acknowledgement (step 20 in sequence diagram).

## Full Test Script

```sql
-- Setup
USE [YourDatabase];
GO
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    Name NVARCHAR(100),
    Salary DECIMAL(10, 2)
);
INSERT INTO Employees VALUES (1, 'Alice', 50000), (2, 'Bob', 60000);
GO

-- Test transaction
BEGIN TRANSACTION;
    UPDATE Employees SET Salary = Salary + 5000 WHERE EmployeeID = 1;

    -- View locks during transaction
    SELECT * FROM sys.dm_tran_locks WHERE request_session_id = @@SPID;

ROLLBACK;  -- Prevent actual change (for testing)
```
