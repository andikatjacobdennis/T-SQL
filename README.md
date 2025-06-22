# T-SQL Learning Resources

Welcome to this T-SQL learning repository! This guide will help you get started with T-SQL (Transact-SQL), Microsoft's powerful database language used in SQL Server.

## View the Learning Materials

You have two options to view the documentation:

#### Option A: View Online

All documentation files are in the `docs/` folder. You can read them directly:

- Open the `docs/` folder
- Start with `index.md`

#### **Option B: Build a Local Documentation Website in VS Code (Advanced Setup)**

If you prefer a **professional, interactive documentation website** (instead of just reading Markdown files), you can build one locally using **MkDocs**. This creates a searchable, well-formatted site with navigation—perfect for learning T-SQL efficiently.

##### **Step 1: Install Python (Required for MkDocs)**

Since MkDocs runs on Python, you need to install it first:

1. **Download Python** (Windows 11):

   - Go to [python.org/downloads](https://www.python.org/downloads/)
   - Download the **latest stable version** (e.g., Python 3.12).
   - **IMPORTANT:** During installation, **check** ☑ **"Add Python to PATH"** before clicking Install.

2. **Verify Python Installation** (in VS Code):
   - Open **VS Code Terminal** (`Ctrl + ~`).
   - Run:
     ```bash
     python --version
     ```
   - Expected output: `Python 3.x.x`

### **Step 2: Clone This Repository in VS Code**

1. **Open VS Code** (`Ctrl + Shift + P` to open Command Palette).
2. **Clone the Repository**:
   - Press `Ctrl + Shift + P` → Type **"Git: Clone"** → Paste:
     ```
     https://github.com/andikatjacobdennis/T-SQL.git
     ```
   - Select a folder (e.g., `C:\Users\%USERPROFILE%\source\repos\T-SQL`).
3. **Open the Project**:
   - Go to **File → Open Folder** → Select the cloned `T-SQL` folder.

### **Step 3: Build the Documentation Site**

Now, generate the website from the Markdown files:

1. **Navigate to the Project Folder** (in VS Code Terminal):
   ```bash
   cd C:\Users\%USERPROFILE%\source\repos\T-SQL
   ```
2. **Build the Static Site**:
   ```bash
   mkdocs build
   ```
   - This creates a `site/` folder with HTML files.

### **Step 4: Launch the Local Website**

Instead of opening raw HTML files, use MkDocs' **live-reload server** for a smooth experience:

1. **Start the Local Server**:
   ```bash
   mkdocs serve
   ```
   - Output:
     ```
     INFO    -  Serving on http://127.0.0.1:8000
     ```
2. **Open in Browser**:
   - Press `Ctrl + Click` on [http://127.0.0.1:8000](http://127.0.0.1:8000) (or paste it into your browser).

**Now you have a fully interactive documentation site!**

- **Features**:
  - **Search bar** (find topics instantly).
  - **Sidebar navigation** (easy browsing).
  - **Dark/Light mode** (toggle in settings).
  - **Auto-refresh** (changes update live).

### **Troubleshooting**

🔹 **MkDocs not recognized?** → Restart VS Code or reopen the terminal.  
🔹 **Python not found?** → Reinstall Python with **"Add to PATH"** enabled.  
🔹 **Broken links?** → Run `mkdocs build --strict` to check errors.

### **Why Use MkDocs Instead of Raw Markdown?**

✔ **Better readability** (themed UI).  
✔ **Search functionality** (find commands fast).  
✔ **Responsive design** (works on phones/tablets).  
✔ **Easier navigation** (sidebar, table of contents).

### **Next Steps**

Now that your **local T-SQL documentation site** is running, you can:  
**Study interactively** (better than plain text files).  
**Edit content in VS Code** (changes auto-refresh in the browser).  
**Deploy online** (GitHub Pages, Netlify—see [MkDocs docs](https://www.mkdocs.org/user-guide/deploying-your-docs/)).

**Enjoy your enhanced T-SQL learning experience!**
(Start exploring at [http://127.0.0.1:8000](http://127.0.0.1:8000))

## How to Contribute

Found an error or want to improve something?

1. Click the "Fork" button at the top right
2. Make your changes
3. Click "New Pull Request" to submit your improvements

## License

This content is free to use - see the [LICENSE](LICENSE) file for details.
