# T-SQL

Welcome to this T-SQL learning repository! This guide will help you get started with T-SQL (Transact-SQL), Microsoft's powerful database language used in SQL Server.

## View the Learning Materials

### Option A: Read Markdown Files Directly

All documentation files are in the `docs/` folder:

- Open the `docs/` directory
- Start with `index.md`

### Option B: Build Interactive Documentation Website (Recommended)

Create a professional, searchable documentation site locally using MkDocs:

#### Prerequisites

1. **Python 3.8+** ([python.org/downloads](https://www.python.org/downloads/))
   - Check "Add Python to PATH" during installation
2. **VS Code** (or any terminal)
3. **Git** (for cloning)

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

#### Key Features

✔ **Instant search** across all documentation
✔ **Dark/light mode** toggle
✔ **Mobile-responsive** design
✔ **Auto-refresh** when files change
✔ **PDF export** (via browser print)

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
