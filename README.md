# T-SQL

This repository contains comprehensive documentation and learning resources for T-SQL (Transact-SQL), Microsoft's extension to the SQL language used in SQL Server. The materials cover everything from basic concepts to advanced features, including practical examples and command references.

## Repository Structure

```
T-SQL/
├── docs/                                # Documentation files
│   ├── images/                          # Supporting images
│   │   ├── DatabaseManagementSystems.jpg
│   │   ├── Edgar_F_Codd.jpg
│   │   ├── erd.png
│   │   └── History_Of_SQL_To_Modern_T-SQL.png
│   ├── puml/                            # PlantUML source files
│   │   └── erd.puml
│   ├── 001_History_of_SQL_to_modern_T_SQL.md
│   ├── 002_Getting_Started.md
│   ├── 003_Installation.md
│   ├── 004_SQL_Server_Management_Studio_SSMS_Walkthrough.md
│   ├── 005_T_SQL_DDL_Data_Definition_Language_Commands.md
│   ├── 006_T_SQL_DML_Data_Manipulation_Language_Commands.md
│   ├── 007_T_SQL_DOL_Data_Query_Language_Commands.md
│   ├── 008_T_SQL_TCL_Transaction_Control_Language_Commands.md
│   ├── 009_T_SQL_DCL_Data_Control_Language_Commands.md
│   ├── 010_Indexing_in_T_SQL.md
│   ├── 011_T_SQL_Practice_Problems.md
│   ├── 012_Frequently_Asked_Questions.md
│   ├── 013_Glossary_of_key_Terms.md
│   └── index.md
├── site/                                # Generated documentation site
├── .gitignore                           # Git ignore rules
├── LICENSE                              # License file
├── mkdocs.yml                           # MkDocs configuration
└── README.md                            # This file
```

## Documentation Contents

The documentation is organized into the following sections:

1. **History of SQL to modern T-SQL** - Evolution of the language
2. **Getting Started** - Introduction to T-SQL concepts
3. **Installation** - Setting up SQL Server and tools
4. **SSMS Walkthrough** - Using SQL Server Management Studio
5. **DDL Commands** - Data Definition Language (CREATE, ALTER, DROP)
6. **DML Commands** - Data Manipulation Language (INSERT, UPDATE, DELETE)
7. **DQL Commands** - Data Query Language (SELECT)
8. **TCL Commands** - Transaction Control Language (COMMIT, ROLLBACK)
9. **DCL Commands** - Data Control Language (GRANT, REVOKE)
10. **Indexing** - Performance optimization techniques
11. **Practice Problems** - Hands-on exercises
12. **FAQ** - Common questions and answers
13. **Glossary** - Key terms and definitions

## How to Use This Repository

1. **Browse the documentation** - Navigate through the markdown files in the `docs/` directory
2. **Build the site locally** (requires MkDocs):
   ```
   mkdocs build
   ```
3. **Serve the documentation locally**:
   ```
   mkdocs serve
   ```
4. **Contribute** - Submit pull requests or issues for improvements

## Requirements

To build the documentation site locally:

- Python 3.x
- MkDocs (`pip install mkdocs`)
- Any MkDocs themes/plugins specified in `mkdocs.yml`

## License

This project is licensed under the terms of the [LICENSE](LICENSE) file.

## Contributing

Contributions are welcome! Please follow the standard GitHub workflow:

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Submit a pull request

For major changes, please open an issue first to discuss what you would like to change.
