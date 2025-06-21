## SQL Server Management Studio (SSMS) – Walkthrough

### **Step 1: Launch SSMS & Connect to Server**

#### Description:

Open SSMS and connect to a SQL Server instance.

#### 📌 Actions:

* Open SSMS from Start Menu.
* In the **Connect to Server** dialog:

  * Server type: `Database Engine`
  * Server name: `localhost` or `.\SQLEXPRESS`
  * Authentication: `Windows Authentication` or `SQL Server Authentication`
* Click **Connect**.

> *\[Screenshot Placeholder: Connect to Server Dialog]*

### **Step 2: Explore Object Explorer**

#### Description:

Navigate database objects like tables, views, procedures, and logins.

#### 📌 Actions:

* On the left side, locate **Object Explorer**.
* Expand:

  * `Databases` → `YourDatabaseName` → `Tables`, `Views`, etc.
  * `Security` → Manage logins and roles
  * `Server Objects` for backups, linked servers, etc.

> *\[Screenshot Placeholder: Object Explorer Panel]*

### **Step 3: Open New Query Window**

#### Description:

Write and run SQL or T-SQL code.

#### 📌 Actions:

* Click **New Query** in the toolbar.
* Select a database from the dropdown.
* Type a query, e.g.,

  ```sql
  SELECT * FROM Customers;
  ```
* Click **Execute** or press `F5`.

> *\[Screenshot Placeholder: Query Editor Window]*

### **Step 4: View Results & Messages**

#### Description:

See the output of your query and messages from the server.

#### 📌 Actions:

* After execution, view:

  * **Results** tab (data grid)
  * **Messages** tab (status, row count, errors)

> *\[Screenshot Placeholder: Results and Messages Pane]*

### **Step 5: Use Toolbar Commands**

#### Description:

Quick-access actions like parsing, executing, saving scripts, etc.

#### 📌 Actions:

* Use buttons:

  * `Execute` (▶)
  * `Parse` (✓)
  * `Cancel` (■)
  * `Database dropdown`
  * `Save`, `Open`, `New Query`

> *\[Screenshot Placeholder: SSMS Toolbar]*

### **Step 6: View Properties & Output Panels (Optional)**

#### Description:

Inspect selected object properties or see output logs.

#### 📌 Actions:

* Right-click on a table → **Properties**
* View output of backups, deployments, etc. in **Output Panel**
* Check **Error List** for issues in scripts

> *\[Screenshot Placeholder: Properties Panel / Error List]*

### **Step 7: Use Solution Explorer or Template Explorer (Optional)**

#### Description:

Manage SQL script projects or use built-in templates.

#### 📌 Actions:

* Open from View menu:

  * **Solution Explorer**: Organize scripts/projects
  * **Template Explorer**: Use predefined T-SQL templates (e.g., CREATE TABLE)

> *\[Screenshot Placeholder: Solution & Template Explorer]*
