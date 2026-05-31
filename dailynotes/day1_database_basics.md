# Day 1 — Database Basics & Types

## What is a Database?
A database is an organized collection of data stored and accessed electronically.

*Structure:*
SERVER
├── Database (Sales)
│   ├── Schema (Orders)
│   └── Schema (Customers)
└── Database (HR)

---

## SQL vs NoSQL

| | SQL | NoSQL |
|---|---|---|
| Structure | Tables (rows & columns) | Flexible |
| Example | MySQL, PostgreSQL | MongoDB, Redis |
| Best for | Structured data | Large/unstructured data |

---

## Database Types

### 1. Relational (SQL)
- Data stored in tables — rows & columns (like a spreadsheet)
- Tables are connected to each other
- Example tools: **MySQL, PostgreSQL, Microsoft SQL Server**

### 2. Key-Value (NoSQL)
- Data stored as key → value pairs
- Like a big dictionary
- Example tools: **Redis, Amazon DynamoDB**

### 3. Column-Based (NoSQL)
- Data stored column by column
- Used when data is very large
- Best for: searching & analytics on huge datasets
- Example tools: **Apache Cassandra, Amazon Redshift**

### 4. Document (NoSQL)
- Data stored as documents (like JSON)
- Doesn't care about structure
- Example tools: **MongoDB**

### 5. Graph (NoSQL)
- Focus is on connections between data points
- Best for: social networks, recommendations
- Example tools: **Neo4j**

---

## SQL Data Types (Basics)

| Type | Examples | Use |
|---|---|---|
| INT | 1, 2, 30 | Whole numbers |
| DECIMAL | 3.14, 100.50 | Decimal numbers |
| CHAR | 'M' | Fixed length text |
| VARCHAR | 'Maria', 'E5A6' | Variable length text |

---

## Key Takeaway
> Relational DB = Tables + SQL
> Everything else = NoSQL
