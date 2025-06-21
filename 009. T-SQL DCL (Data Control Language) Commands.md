# 009. T-SQL DCL (Data Control Language) Commands

DCL (Data Control Language) commands manage database security by controlling access to database objects through permissions and roles.

## 1. User and Login Management

### Create Logins and Users
```sql
-- Create a SQL Server login
CREATE LOGIN [SalesManager] 
WITH PASSWORD = 'Str0ngP@ssw0rd!',
     DEFAULT_DATABASE = [OrderDB],
     CHECK_EXPIRATION = ON,
     CHECK_POLICY = ON;
GO

-- Create a database user mapped to login
USE [OrderDB];
CREATE USER [SalesManager_User] FOR LOGIN [SalesManager];
GO

-- Create a user without login (for application use)
CREATE USER [App_Service_Account] WITHOUT LOGIN;
GO
```

### Modify Users
```sql
-- Change user name
ALTER USER [SalesManager_User] WITH NAME = [SalesAdmin_User];
GO

-- Change default schema
ALTER USER [SalesAdmin_User] WITH DEFAULT_SCHEMA = [Sales];
GO

-- Map user to different login
ALTER USER [SalesAdmin_User] WITH LOGIN = [NewSalesLogin];
GO
```

### Remove Users and Logins
```sql
-- Drop database user
DROP USER [App_Service_Account];
GO

-- Drop server login
DROP LOGIN [SalesManager];
GO
```


## 2. Role Management

### Server Roles
```sql
-- Add login to fixed server role
ALTER SERVER ROLE [sysadmin] ADD MEMBER [SalesManager];
GO

-- Create custom server role
CREATE SERVER ROLE [OrderDB_Admin];
GO
GRANT CONTROL SERVER TO [OrderDB_Admin];
GO
```

### Database Roles
```sql
-- Add user to fixed database role
ALTER ROLE [db_datareader] ADD MEMBER [SalesAdmin_User];
GO

-- Create custom database role
CREATE ROLE [Sales_Team];
GO

-- Grant role to another role
ALTER ROLE [Sales_Team] ADD MEMBER [Marketing_Team];
GO

-- Drop role
DROP ROLE [Sales_Team];
GO
```


## 3. Permission Management

### Grant Permissions
```sql
-- Basic permissions
GRANT SELECT ON [Sales].[Customers] TO [Sales_Team];
GRANT INSERT, UPDATE ON [Sales].[Orders] TO [SalesAdmin_User];
GRANT EXECUTE ON [Sales].[PlaceOrder] TO [Sales_Team];

-- Schema-level permissions
GRANT SELECT, INSERT ON SCHEMA::[Sales] TO [Sales_Team];
GRANT ALTER ON SCHEMA::[Sales] TO [SalesAdmin_User];

-- Database-level permissions
GRANT CREATE TABLE TO [SalesAdmin_User];
GRANT SHOWPLAN TO [Reporting_User];
```

### Deny Permissions
```sql
-- Explicit deny overrides grants
DENY DELETE ON [Sales].[Customers] TO [Sales_Team];
DENY ALTER ON SCHEMA::[Finance] TO [SalesAdmin_User];
```

### Revoke Permissions
```sql
-- Remove specific permissions
REVOKE SELECT ON [Sales].[Customers] FROM [Sales_Team];
REVOKE CREATE TABLE FROM [SalesAdmin_User];

-- Remove all permissions
REVOKE ALL ON [Sales].[Orders] FROM [Sales_Team];
```


## 4. Row-Level Security (RLS)

### Create Security Policies
```sql
-- Create predicate function
CREATE FUNCTION [Sales].[fn_SecurityPredicate](@SalesRepID INT)
RETURNS TABLE
WITH SCHEMABINDING
AS RETURN
    SELECT 1 AS [result]
    WHERE @SalesRepID = USER_ID()
    OR USER_NAME() = 'SalesManager';
GO

-- Apply security policy
CREATE SECURITY POLICY [Sales].[CustomerAccessPolicy]
ADD FILTER PREDICATE [Sales].[fn_SecurityPredicate](SalesRepID)
ON [Sales].[Customers];
GO

-- Alter security policy
ALTER SECURITY POLICY [Sales].[CustomerAccessPolicy]
ADD BLOCK PREDICATE [Sales].[fn_SecurityPredicate](SalesRepID)
ON [Sales].[Customers] AFTER INSERT;
GO
```

### Manage RLS
```sql
-- Disable policy
ALTER SECURITY POLICY [Sales].[CustomerAccessPolicy] WITH (STATE = OFF);
GO

-- Drop policy
DROP SECURITY POLICY [Sales].[CustomerAccessPolicy];
GO
```


## 5. Dynamic Data Masking (DDM)

### Implement Data Masking
```sql
-- Add masking to existing column
ALTER TABLE [Sales].[Customers]
ALTER COLUMN [Email] ADD MASKED WITH (FUNCTION = 'email()');
GO

-- Full masking options
ALTER TABLE [HR].[Employees]
ALTER COLUMN [Salary] ADD MASKED WITH (FUNCTION = 'random(10000, 50000)');
GO

ALTER TABLE [Sales].[Customers]
ALTER COLUMN [CreditCard] ADD MASKED WITH (FUNCTION = 'partial(0, "XXXX-XXXX-XXXX-", 4)');
GO
```

### Manage Masking
```sql
-- Grant unmask permission
GRANT UNMASK TO [Finance_Team];
GO

-- Remove masking
ALTER TABLE [Sales].[Customers]
ALTER COLUMN [Email] DROP MASKED;
GO
```


## 6. Auditing and Compliance

### Create Server Audit
```sql
-- Create audit destination
CREATE SERVER AUDIT [OrderDB_Audit]
TO FILE (FILEPATH = 'C:\Audits\', MAXSIZE = 1 GB)
WITH (QUEUE_DELAY = 1000, ON_FAILURE = CONTINUE);
GO

-- Enable audit
ALTER SERVER AUDIT [OrderDB_Audit] WITH (STATE = ON);
GO
```

### Database Audit Specification
```sql
-- Track DDL changes
CREATE DATABASE AUDIT SPECIFICATION [OrderDB_DDL_Audit]
FOR SERVER AUDIT [OrderDB_Audit]
ADD (SCHEMA_OBJECT_CHANGE_GROUP),
ADD (DATABASE_PRINCIPAL_CHANGE_GROUP);
GO

-- Track sensitive data access
ALTER DATABASE AUDIT SPECIFICATION [OrderDB_DDL_Audit]
ADD (SELECT, INSERT, UPDATE, DELETE ON [Sales].[Customers] BY [public]);
GO
```


## 7. Complete Security Example

```sql
-- 1. Create login and user
CREATE LOGIN [Audit_Admin] WITH PASSWORD = 'Aud1tP@ss!';
GO
USE [OrderDB];
CREATE USER [Audit_Admin] FOR LOGIN [Audit_Admin];
GO

-- 2. Create custom role
CREATE ROLE [Data_Stewards];
GO

-- 3. Assign permissions
GRANT SELECT ON SCHEMA::[Sales] TO [Data_Stewards];
GRANT INSERT ON [Sales].[Customers] TO [Data_Stewards];
DENY DELETE ON SCHEMA::[Sales] TO [Data_Stewards];
GO

-- 4. Add user to role
ALTER ROLE [Data_Stewards] ADD MEMBER [Audit_Admin];
GO

-- 5. Implement row-level security
CREATE FUNCTION [Sales].[fn_RegionSecurity](@RegionID INT)
RETURNS TABLE WITH SCHEMABINDING
AS RETURN (SELECT 1 AS [access] 
           WHERE @RegionID = (SELECT RegionID FROM [emp].[RegionMap] 
                              WHERE UserID = USER_ID()));
GO

CREATE SECURITY POLICY [Sales].[RegionPolicy]
ADD FILTER PREDICATE [Sales].[fn_RegionSecurity](RegionID) ON [Sales].[Orders];
GO

-- 6. Set up auditing
CREATE SERVER AUDIT [SensitiveData_Access]
TO APPLICATION_LOG
WITH (QUEUE_DELAY = 1000);
GO

CREATE DATABASE AUDIT SPECIFICATION [CustomerData_Access]
FOR SERVER AUDIT [SensitiveData_Access]
ADD (SELECT, UPDATE ON [Sales].[Customers] BY [public]);
GO
```


## DCL Best Practices
1. Principle of Least Privilege: Grant minimum required permissions
2. Use Roles: Manage permissions via roles, not individual users
3. Regular Reviews: Audit permissions quarterly
4. Secure Defaults: Rename/disable 'sa' account, disable guest user
5. Documentation: Maintain permission matrix
6. Test Changes: Verify permissions in non-production first
