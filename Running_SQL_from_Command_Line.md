### Prerequisites
1. **SQL Server**: Make sure SQL Server is installed on your system.
2. **SQLCMD Tool**: Ensure SQLCMD is installed. It comes with SQL Server installations or can be installed separately via the SQL Server feature pack.

### Steps to Run SQL from CMD

1. **Open Command Prompt**:
   - Press `Win + R`, type `cmd`, and press `Enter` to open Command Prompt.

2. **Verify SQLCMD Installation**:
   - Type `sqlcmd -?` and press `Enter` to check if SQLCMD is installed and accessible. You should see the help options for SQLCMD.

3. **Connect to SQL Server**:
   - To connect to a SQL Server instance, use the following command format:
     ```cmd
     sqlcmd -S server_name -U user_name -P password
     ```
   - **Parameters**:
     - `-S` specifies the server name (e.g., `localhost` or `.\SQLEXPRESS` for a local SQL Server Express instance).
     - `-U` specifies the user name.
     - `-P` specifies the password.

   - If using Windows Authentication, use:
     ```cmd
     sqlcmd -S server_name -E
     ```
     - `-E` uses the current Windows user credentials to connect.

4. **Execute SQL Commands**:
   - Once connected, you can start executing SQL commands directly in the SQLCMD prompt. For example:
     ```sql
     SELECT * FROM your_table;
     GO
     ```

5. **Run SQL from a File**:
   - To execute SQL commands from a file, use:
     ```cmd
     sqlcmd -S server_name -U user_name -P password -i path_to_sql_file.sql
     ```
   - **Parameters**:
     - `-i` specifies the input file containing the SQL commands.

   - For Windows Authentication, use:
     ```cmd
     sqlcmd -S server_name -E -i path_to_sql_file.sql
     ```

6. **Redirect Output to a File**:
   - To save the output of your SQL commands to a file, use:
     ```cmd
     sqlcmd -S server_name -U user_name -P password -i path_to_sql_file.sql -o path_to_output_file.txt
     ```
   - **Parameters**:
     - `-o` specifies the output file path.

7. **Exit SQLCMD**:
   - Type `EXIT` or `QUIT` and press `Enter` to exit the SQLCMD prompt.

### Example Commands
1. **Connect using SQL Server Authentication**:
   ```cmd
   sqlcmd -S localhost -U sa -P MyPassword123
   ```

2. **Connect using Windows Authentication and run a file**:
   ```cmd
   sqlcmd -S localhost -E -i C:\scripts\my_script.sql
   ```

3. **Run a SQL command and save output**:
   ```cmd
   sqlcmd -S localhost -E -Q "SELECT * FROM my_table" -o C:\output\results.txt
   ```
