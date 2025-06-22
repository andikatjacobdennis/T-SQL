# T-SQL

Welcome to this T-SQL learning repository! This guide will help you get started with T-SQL (Transact-SQL), Microsoft's powerful database language used in SQL Server.

## View the Learning Materials

### Option A: Read Markdown Files Directly

All documentation files are in the `docs/` folder:

- Open the `docs/` directory
- Start with `index.md`

### Option B: Build Interactive Documentation Website (Recommended)

Create a professional, searchable documentation site locally using MkDocs:

#### **Prerequisites**

1. **Python 3.8+**

   - **Download**: [python.org/downloads](https://www.python.org/downloads/)
   - **Important**: Check ✅ **"Add Python to PATH"** during installation.
   - **Verify Installation**: Run `python --version` in the terminal.

2. **VS Code (Recommended Editor)**

   - **Download**: [code.visualstudio.com](https://code.visualstudio.com/)

3. **Git (for version control & cloning)**
   - **Download**: [git-scm.com](https://git-scm.com/downloads)
   - **Verify Installation**: Run `git --version` in the terminal.

#### Setup Instructions

1. **Clone the Repository**

   ```bash
   git clone https://github.com/andikatjacobdennis/T-SQL.git
   cd T-SQL
   ```

2. **Set Up Python Environment**

   ```bash
   python.exe -m pip install --upgrade pip
   pip install mkdocs mkdocs-material mkdocs-minify-plugin
   ```

3. **Build and Serve the Documentation**
   ```bash
   mkdocs serve
   ```
   - Access at: [http://127.0.0.1:8000](http://127.0.0.1:8000)

## Troubleshooting

| Issue                 | Solution                                                                            |
| --------------------- | ----------------------------------------------------------------------------------- |
| MkDocs not found      | Run `python -m pip install --upgrade mkdocs`                                        |
| Plugin errors         | Reinstall plugins: `pip install --force-reinstall mkdocs-tags mkdocs-minify-plugin` |
| Python not recognized | Reinstall Python with PATH option                                                   |
| Broken links          | Run `mkdocs build --strict`                                                         |

## Advanced Usage

### Build Static Site

```bash
mkdocs build --clean
```

Outputs to `site/` directory

### Deploy to GitHub Pages

```bash
mkdocs gh-deploy
```

## Contributing

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Open a Pull Request

## License

Open-source under [MIT License](LICENSE)
