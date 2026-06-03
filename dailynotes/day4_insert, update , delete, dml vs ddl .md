# Day 4 --> INSERT, UPDATE, DELETE (DML vs DDL)

So today is all about DML — Data Manipulation Language.
If DDL was about building the structure, DML is about filling it and managing it.
These are the commands you'll use the most in real life.

---

## INSERT — Adding New Data

When your table is ready and you want to put data into it, you use INSERT.

```sql
-- Insert a single row
INSERT INTO customers (customer_id, name, city)
VALUES (1, 'Aman', 'Delhi');

-- Insert multiple rows at once
INSERT INTO customers (customer_id, name, city)
VALUES
(1, 'Aman', 'Delhi'),
(2, 'Priya', 'Mumbai');
```

**Things to remember:**
- Column names and values must match in the **same order**
- If you're inserting values for ALL columns, you can skip column names
- Text values go in **single quotes** `'like this'`
- Numbers don't need quotes

```sql
-- Shorthand (only if inserting all columns in order)
INSERT INTO customers VALUES (3, 'Riya', 'Noida');
```
## UPDATE — Changing Existing Data

When data already exists but needs to be changed, use UPDATE.
Real life example — a customer moved to another city.

```sql
-- Update a specific row
UPDATE customers
SET city = 'Bangalore'
WHERE customer_id = 2;

-- Update multiple columns at once
UPDATE customers
SET city = 'Delhi', phone = '9999999999'
WHERE customer_id = 1;
```

> ⚠️ Always use WHERE with UPDATE.
> Without WHERE — it updates **every single row** in the table. Classic mistake.

```sql
-- This updates ALL rows (probably not what you want!)
UPDATE customers SET city = 'Delhi';
```

---

## DELETE — Removing Data

When you want to remove specific rows from a table, use DELETE.

```sql
-- Delete a specific row
DELETE FROM customers WHERE customer_id = 1;

-- Delete multiple rows
DELETE FROM customers WHERE city = 'Noida';
```

> ⚠️ Same rule — always use WHERE with DELETE.
> Without WHERE — it deletes **every row** in the table.

```sql
-- This deletes ALL rows (dangerous!)
DELETE FROM customers;
```

---

## TRUNCATE — Full Wipe

Removes ALL rows from a table instantly but keeps the structure.

```sql
TRUNCATE TABLE students;
```

**Important points:**
- No WHERE clause allowed — can't delete specific rows
- Faster than DELETE — doesn't go row by row, wipes everything at once
- Cannot be rolled back — once done, data is gone permanently
- Resets auto-increment — IDs start from 1 again after truncate

---

## TRUNCATE vs DELETE

| Feature | TRUNCATE | DELETE |
|---------|----------|--------|
| Removes all rows | ✅ Yes | ✅ Yes |
| Removes specific rows | ❌ No | ✅ Yes (with WHERE) |
| Speed | ⚡ Fast | 🐢 Slow |
| WHERE clause | ❌ Not allowed | ✅ Allowed |
| Rollback | ❌ No | ✅ Yes |
| Auto increment reset | ✅ Yes | ❌ No |
| Type | DDL | DML |

> Easy way to remember:
> - DELETE → smart cleaning (you choose what goes)
> - TRUNCATE → full wipe (everything gone, no questions asked)

---
## DDL vs DML — The Big Difference

| | DDL | DML |
|--|-----|-----|
| Full form | Data Definition Language | Data Manipulation Language |
| Works on | Tables / Columns (structure) | Rows (data) |
| Commands | CREATE, ALTER, DROP, TRUNCATE | INSERT, UPDATE, DELETE |
| Rollback | ❌ No | ✅ Yes |
| Purpose | Design the database | Fill and manage the data |

**DDL examples:**
```sql
CREATE TABLE students (...);   -- build structure
ALTER TABLE students ADD age INT;  -- edit structure
DROP TABLE students;           -- delete structure
```

**DML examples:**
```sql
INSERT INTO students VALUES (...);         -- add rows
UPDATE students SET age = 20 WHERE id = 1; -- edit rows
DELETE FROM students WHERE id = 2;         -- remove rows



