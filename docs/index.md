# Introduction

Welcome to this T-SQL tutorial, where we’ll take you from the foundations of SQL to modern Transact-SQL (T-SQL) used in Microsoft SQL Server. Whether you're a beginner or looking to refine your skills, this guide will walk you through essential concepts, commands, and best practices.

We’ll start with the history and evolution of SQL, then move into installation, SQL Server Management Studio (SSMS) setup, and core T-SQL commands—covering DDL, DML, DQL, TCL, and DCL. You’ll also learn about indexing for performance optimization.

By the end, you’ll have a solid grasp of T-SQL to query, manipulate, and manage databases efficiently. Let’s get started!

## Table of Contents

### Foundations & Setup

- [001. History of SQL to Modern T-SQL](001_History_of_SQL_to_modern_T_SQL.md)
- [002. Getting Started](002_Getting_Started.md)
- [003. Installation](003_Installation.md)
- [004. SQL Server Management Studio (SSMS) – Walkthrough](004_SQL_Server_Management_Studio_SSMS_Walkthrough.md)

### Core T-SQL Language

- [005. T-SQL DDL (Data Definition Language) Commands](005_T_SQL_DDL_Data_Definition_Language_Commands.md)
- [006. T-SQL DML (Data Manipulation Language) Commands](006_T_SQL_DML_Data_Manipulation_Language_Commands.md)
- [007. T-SQL DQL (Data Query Language) Commands](007_T_SQL_DQL_Data_Query_Language_Commands.md)
- [008. T-SQL TCL (Transaction Control Language) Commands](008_T_SQL_TCL_Transaction_Control_Language_Commands.md)
- [009. T-SQL DCL (Data Control Language) Commands](009_T_SQL_DCL_Data_Control_Language_Commands.md)

### Advanced Topics

#### Performance Optimization

- [010. Indexing in T-SQL](010_Indexing_in_T_SQL.md)
  - Clustered vs. Non-Clustered Indexes
  - Index Maintenance (Rebuild/Reorganize)
  - Covering Indexes and Included Columns
- [011. Query Performance Tuning](011_Query_Performance_Tuning.md)
  - Execution Plans (Actual vs. Estimated)
  - Statistics and Cardinality Estimation
  - Parameter Sniffing and Optimization Hints

#### Data Integrity & Security

- [012. Constraints and Triggers](012_Constraints_and_Triggers.md)
  - Advanced Constraint Types (CHECK, UNIQUE, FOREIGN KEY)
  - INSTEAD OF vs. AFTER Triggers
- [013. Row-Level Security (RLS) & Dynamic Data Masking](013_Row_Level_Security_and_Dynamic_Data_Masking.md)
  - Implementing RLS with Security Policies
  - Masking Sensitive Data (Partial, Random, Default Masks)

#### Advanced Query Techniques

- [014. Window Functions & Advanced Aggregation](014_Window_Functions_and_Advanced_Aggregation.md)
  - `PARTITION BY`, `ORDER BY`, and Framing (ROWS/RANGE)
  - `LEAD()`, `LAG()`, `FIRST_VALUE()`, and `NTILE()`
- [015. Common Table Expressions (CTEs) & Recursive Queries](015_CTEs_and_Recursive_Queries.md)
  - Hierarchical Data (Employee/Org Charts)
  - Graph Processing with Recursive CTEs

#### Error Handling & Transactions

- [016. TRY-CATCH & Custom Error Handling](016_TRY_CATCH_and_Custom_Error_Handling.md)
  - `THROW` vs. `RAISERROR`
  - Custom Error Logging
- [017. Transaction Isolation Levels](017_Transaction_Isolation_Levels.md)
  - Read Uncommitted to Serializable
  - Deadlock Prevention Strategies

#### Temporal & Spatial Data

- [018. Temporal Tables (Time-Travel Queries)](018_Temporal_Tables.md)
  - System-Versioned Tables
  - Querying Historical Data with `FOR SYSTEM_TIME`
- [019. Spatial Data in T-SQL](019_Spatial_Data_in_T_SQL.md)
  - `GEOGRAPHY` vs. `GEOMETRY`
  - Distance, Intersection, and Buffer Queries

#### Automation & Dynamic SQL

- [020. Dynamic SQL & Stored Procedures](020_Dynamic_SQL_and_Stored_Procedures.md)
  - Safe Execution with `sp_executesql`
  - SQL Injection Mitigation
- [021. SQL Agent Jobs & Automation](021_SQL_Agent_Jobs_and_Automation.md)
  - Scheduling Maintenance Tasks
  - Alerting and Notifications

### Practice

- [022. T-SQL Practice Problems](022_T_SQL_Practice_Problems.md)

### Appendix

- [023. Frequently Asked Questions](023_Frequently_Asked_Questions.md)
- [024. Glossary of Key Terms](024_Glossary_of_Key_Terms.md)
