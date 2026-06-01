# Week 1 — Day 2 · SQL Command Types & Data Types

## Why SQL?
- **Talk to Data** — SQL lets you communicate with databases storing massive amounts of data
- **High Demand** — used by Software Developers, Data Analysts, Data Scientists, Data Engineers
- **Industry Standard** — powers tools like Power BI, Tableau, Kafka, Spark, Azure Synapse

---

## Types of SQL Commands

SQL commands are grouped by what they do:

### 1. DDL — Data Definition Language
> Used when the server/table is empty and you want to **define or change its structure**

| Command | What it does |
|--------|--------------|
| `CREATE` | Creates a new table or database |
| `ALTER` | Modifies an existing table/object |
| `DROP` | Deletes a table or database entirely |
| `TRUNCATE` | Removes all rows from a table quickly (keeps structure) |

---

### 2. DML — Data Manipulation Language
> Used when a website or app is generating data and you want to **push that data into the server**

| Command | What it does |
|--------|--------------|
| `INSERT` | Adds new records to a table |
| `UPDATE` | Modifies existing records |
| `DELETE` | Removes records |

---

### 3. DQL — Data Query Language
> Used when data is already in the server and you want to **ask it questions / fetch answers**

| Command | What it does |
|--------|--------------|
| `SELECT` | Fetches data from one or more tables (`*` = all columns) |

> 💡 DQL is the **most used** type in day-to-day SQL work

---

### 4. DCL — Data Control Language *(optional for now)*
> Controls who has access to what

| Command | What it does |
|--------|--------------|
| `GRANT` | Gives a user permission |
| `REVOKE` | Takes away a user's permission |

> DCL is the **least used** type — more relevant in admin/DevOps roles

---

### Quick Summary Table

| Type | Full Name | Commands | Used for |
|------|-----------|----------|----------|
| DDL | Data Definition Language | CREATE, ALTER, DROP, TRUNCATE | Structure |
| DML | Data Manipulation Language | INSERT, UPDATE, DELETE | Data in/out |
| DQL | Data Query Language | SELECT | Querying |
| DCL | Data Control Language | GRANT, REVOKE | Permissions |

---

## SQL Data Types

Data types define what kind of data can be stored in each column.

| Data Type | Description | Example |
|-----------|-------------|---------|
| `VARCHAR(n)` | Stores text/characters | `'Priya'`, `'Mumbai'` |
| `INTEGER` | Stores whole numbers | `1`, `2`, `4` |
| `DATE` | Stores calendar dates | `2023-05-01` |
| `BOOLEAN` | Stores True/False values | `TRUE`, `FALSE` |
| `FLOAT` | Stores decimal numbers | `3.14`, `9.99` |
| `TEXT` | Stores long text | Long descriptions |
| `TIMESTAMP` | Stores date + time | `2023-05-01 10:30:00` |

---

> **The Flow:** Empty server → DDL (create structure) → DML (fill with data) → DQL (query the data)
