# Installation

## **Part 1: Installing Microsoft SQL Server**

### 1. **Download SQL Server**

* Go to the official page:
  🔗 [https://www.microsoft.com/en-us/sql-server/sql-server-downloads](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)
* Choose the edition:

  * **Developer** (free, full features for learning/testing)
  * **Express** (free, lightweight)
* Click **Download now** under your preferred edition.

---

### 2. **Run the Installer**

* Launch the downloaded installer (e.g., `SQL2019-SSEI-Dev.exe`).
* Choose **Basic** installation for easiest setup, or **Custom** for more control.

---

### 3. **Install SQL Server**

* Accept license terms.
* Choose installation location.
* Click **Install** – the installer will download required files and install the engine.
* When done, note the **instance name** (default is `SQLEXPRESS` or `MSSQLSERVER`).

---

### 4. **Configure SQL Server (if using Custom)**

* If you chose **Custom**, SQL Server Installation Center opens.
* Use the wizard to:

  * Select **New SQL Server stand-alone installation**.
  * Choose **Database Engine Services**.
  * Specify instance name.
  * Set **authentication mode**: use **Mixed Mode** for both Windows and SQL logins.
  * Set `sa` password (remember this).

---

## **Part 2: Installing SSMS (SQL Server Management Studio)**

### 1. **Download SSMS**

* Visit:
  🔗 [https://aka.ms/ssmsfullsetup](https://aka.ms/ssmsfullsetup)
* Download the installer (`SSMS-Setup-*.exe`).

---

### 2. **Install SSMS**

* Run the installer.
* Choose the install location (or leave default).
* Click **Install**.
* After installation, restart if prompted.

---

## **Part 3: Connecting to SQL Server**

### 1. **Launch SSMS**

* Open **SQL Server Management Studio** from the Start menu.

### 2. **Connect to Database Engine**

* **Server type**: Database Engine
* **Server name**:

  * For default instance: `localhost`
  * For named instance: `localhost\SQLEXPRESS` or your custom name
* **Authentication**:

  * **Windows Authentication** (uses your Windows user account)
  * Or **SQL Server Authentication** if you set it up (`sa` user)

### 3. **Click Connect** — you're now inside SQL Server!

---

## **Optional Configuration Tips**

* Enable TCP/IP in **SQL Server Configuration Manager** if you need remote access.
* Use **SQL Server Services** tool to start/stop SQL Server or SQL Agent.
