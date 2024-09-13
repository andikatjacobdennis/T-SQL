### **Step 1: Download SQL Server Express**

#### Practical:
1. **Go to the SQL Server Downloads page**:
   - Visit [SQL Server Downloads](https://www.microsoft.com/en-us/sql-server/sql-server-downloads).
   - ![Screenshot of SQL Server Downloads page placeholder]
2. **Download SQL Server Express**:
   - Scroll to "SQL Server 2022 Express" and click **Download now**.
   - ![Screenshot of SQL Server 2022 Express download placeholder]
3. **Run the installer**:
   - Locate the downloaded .exe file in your Downloads folder and double-click to run the installer.
   - ![Screenshot of running the installer placeholder]
4. **Choose Installation Type**:
   - You’ll see options for **Basic**, **Custom**, or **Download Media**. Select **Basic** for a quick installation.
   - ![Screenshot of installation type selection placeholder]
5. **Accept License Terms**:
   - Read and accept the Microsoft License Agreement by checking the box and clicking **Next**.
   - ![Screenshot of license terms placeholder]
6. **Choose Install Path**:
   - You can change the path or leave it as default and click **Install**.
   - ![Screenshot of install path selection placeholder]
7. **Installation Process**:
   - Wait for the process to finish. Once done, you’ll see the installation success screen.
   - ![Screenshot of installation success screen placeholder]

### **Step 2: Install SQL Server Management Studio (SSMS)**

#### Practical:
1. **Download SSMS**:
   - Visit the [SSMS download page](https://learn.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms) and click **Download SSMS**.
   - ![Screenshot of SSMS download page placeholder]
2. **Run the installer**:
   - Find the .exe file and double-click it.
   - ![Screenshot of running SSMS installer placeholder]
3. **Accept License Terms**:
   - Accept the license agreement and click **Install**.
   - ![Screenshot of SSMS license agreement placeholder]
4. **Complete Installation**:
   - Once the installation finishes, click **Close** and open **SQL Server Management Studio** from your Start Menu.
   - ![Screenshot of SSMS installation completion placeholder]

### **Step 3: Open SSMS and Connect to a Server**

#### Practical:
1. **Launch SSMS**:
   - Open **SQL Server Management Studio** from your Start Menu or Desktop.
   - ![Screenshot of launching SSMS placeholder]
2. **Connect to a Server**:
   - The **Connect to Server** window appears automatically.
   - **Server type**: Choose **Database Engine**.
   - **Server name**: Enter (local)\SQLEXPRESS (or the server name used during installation).
   - **Authentication**: Choose **Windows Authentication** or **SQL Server Authentication** (enter username and password).
   - Click **Connect**.
   - ![Screenshot of Connect to Server window placeholder]
3. **Connected Server**:
   - You’ll now see your SQL Server instance connected in the **Object Explorer** panel.
   - ![Screenshot of Object Explorer with connected server placeholder]

### **Step 4: Explore the Object Explorer**

#### Practical:
1. **Navigate the Object Explorer**:
   - On the left-hand side, the **Object Explorer** shows your connected server, databases, security settings, and other items.
   - Expand the server node to see all available databases.
   - ![Screenshot of Object Explorer placeholder]
2. **Right-click on nodes**:
   - Right-click on any node (e.g., **Databases**) to see options such as **New Database**, **Properties**, and **Tasks**.
   - ![Screenshot of right-click options placeholder]

### **Step 5: Create a New Database**

#### Practical:
1. **Right-click the Databases node**:
   - In the Object Explorer, right-click the **Databases** node and select **New Database**.
   - ![Screenshot of New Database option placeholder]
2. **Enter database details**:
   - In the dialog box that opens, type a name for your database (e.g., MyTestDB).
   - ![Screenshot of database name input placeholder]
3. **Configure settings** (Optional):
   - Leave the default options unless you need to change file paths or size settings.
   - ![Screenshot of database settings placeholder]
4. **Create the database**:
   - Click **OK** to create the new database.
   - ![Screenshot of database creation placeholder]
5. **Verify creation**:
   - In the Object Explorer, expand the **Databases** node to see your newly created database.
   - ![Screenshot of newly created database placeholder]

### **Step 6: Explore Database Features**

#### Practical:
1. **Expand the database**:
   - Click the + sign next to your database name in the Object Explorer.
   - ![Screenshot of expanding database placeholder]
2. **Create a new table**:
   - Right-click on the **Tables** folder and select **New Table**.
   - ![Screenshot of New Table option placeholder]
3. **Design a table**:
   - In the **Table Designer**, add columns with names and data types (e.g., ID (int), Name (nvarchar)).
   - Set constraints like **Primary Key** by right-clicking the column and choosing **Set Primary Key**.
   - ![Screenshot of Table Designer placeholder]
4. **Save the table**:
   - Click **File > Save Table_1** and give it a name (e.g., Customers).
   - ![Screenshot of saving table placeholder]
5. **Verify the table**:
   - Go to **Tables**, expand it, and see your table listed.
   - ![Screenshot of table verification placeholder]

### **Step 7: Backup and Restore Databases**

#### Backup a Database:
1. **Right-click the database**:
   - Right-click on your database (e.g., MyTestDB) in Object Explorer.
   - ![Screenshot of backup database option placeholder]
2. **Go to Tasks > Backup**:
   - Choose **Tasks > Back Up...**.
   - ![Screenshot of backup tasks placeholder]
3. **Set Backup Options**:
   - Select the **Backup type** as **Full**.
   - Under **Destination**, choose where to save the backup file.
   - ![Screenshot of backup options placeholder]
4. **Click OK**:
   - Start the backup by clicking **OK**.
   - ![Screenshot of backup completion placeholder]

#### Restore a Database:
1. **Right-click the Databases node**:
   - Right-click **Databases** in Object Explorer and choose **Restore Database...**.
   - ![Screenshot of restore database option placeholder]
2. **Choose the backup file**:
   - Select **Device** and browse to the location of your backup file.
   - ![Screenshot of selecting backup file placeholder]
3. **Verify settings**:
   - Make sure the source database name is correct.
   - ![Screenshot of verify settings placeholder]
4. **Click OK**:
   - Restore the database by clicking **OK**.
   - ![Screenshot of restore completion placeholder]

### **Step 8: Security Management**

#### Practical:
1. **Expand the Security node**:
   - In Object Explorer, expand the **Security** node to manage logins and roles.
   - ![Screenshot of Security node placeholder]
2. **Add a new login**:
   - Right-click on **Logins** and select **New Login**.
   - Enter a **Login name** (e.g., UserTest).
   - Choose **SQL Server Authentication** and enter a password.
   - ![Screenshot of New Login placeholder]
3. **Set database roles**:
   - Under the **User Mapping** tab, assign roles like **db_datareader** or **db_owner** to the user.
   - ![Screenshot of database roles placeholder]
4. **Click OK**:
   - Save the new login and its permissions.
   - ![Screenshot of new login completion placeholder]

### **Step 9: Querying Data (GUI-Based)**

#### Practical:
1. **Right-click a table**:
   - Expand the **Tables** node inside your database.
   - Right-click a table and select **Select Top 1000 Rows** to view data.
   - ![Screenshot of Select Top 1000 Rows placeholder]
2. **Edit data**:
   - Right-click the table and choose **Edit Top 200 Rows** to open an editor and modify data.
   - ![Screenshot of Edit Top 200 Rows placeholder]

### **Step 10: Configure Database Properties**

#### Practical:
1. **Right-click your database**:
   - In Object Explorer, right-click on the database (e.g., MyTestDB).
   - ![Screenshot of database properties option placeholder]
2. **Select Properties**:
   - Choose **Properties** from the dropdown menu.
   - ![Screenshot of selecting properties placeholder]
3. **Explore settings**:
   - In the **Database Properties** window, navigate between tabs such as **Files**, **Options**, and **Permissions** to configure database settings.
   - ![Screenshot of database properties window placeholder]
4. **Click OK**:
   - Apply changes by clicking **OK**.
   - ![Screenshot of applying changes placeholder]

### **Step 11: Set Up Database Diagrams**

#### Practical:
1. **Right-click on Database Diagrams**:
   - Expand your database and right-click on **Database Diagrams**.
   - ![Screenshot of Database Diagrams option placeholder]
2. **Choose New Diagram**:
   - Select **New Database Diagram** from the context menu.
   - ![Screenshot of New Database Diagram placeholder]
3. **Add tables**:
   - In the dialog box, select tables you want to include in the diagram.
   - ![Screenshot of adding tables placeholder]
4. **Save diagram**:
   - Design relationships between tables and save the diagram for future reference.
   - ![Screenshot of saving diagram placeholder]

### **Step 12: Import and Export Data**

#### Practical:
1. **Import Data**:
   - Right-click on the database and choose **Tasks > Import Data**.
   - Use the **Import and Export Wizard** to select data sources (e.g., Excel, CSV).
   - ![Screenshot of Import Data wizard placeholder]
2. **Export Data**:
   - Right-click the database, select **Tasks > Export Data**, and follow the wizard to export data to different formats.
   - ![Screenshot of Export Data wizard placeholder]

### **Step 13: Monitor Server Performance**

#### Practical:
1. **Open Activity Monitor**:
   - Right-click the connected server in the Object Explorer and select **Activity Monitor**.
   - ![Screenshot of Activity Monitor placeholder]
2. **View real-time stats**:
   - The Activity Monitor displays information about processes, CPU usage, and database I/O performance.
   - ![Screenshot of Activity Monitor stats placeholder]
3. **Analyze queries**:
   - Look under the **Processes** tab to monitor running queries.
   - ![Screenshot of analyzing queries placeholder]
