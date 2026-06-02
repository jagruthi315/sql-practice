## Day 3 --> CREATE, ALTER, DROP, TRUNCATE

So today we go deeper into DDL commands — these are the commands that deal
with the **structure** of your database, not the data inside it.
Think of it like this — DDL is the **blueprint**, DML is the **furniture**.

---

## CREATE — Building Something From Scratch

When your database is empty and you want to set up a new table, you use CREATE.
It's literally just telling SQL "hey, make me a table with these columns."

```sql
CREATE TABLE students (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    age INT,
    city VARCHAR(50),
    enrolled_date DATE
);
```

**Things to remember:**
- Every table needs a **PRIMARY KEY** — a unique ID for each row (like a roll number)
- You define the column name + data type together
- Once created, the table is empty — no data yet, just the structure

---

## ALTER — Editing What Already Exists

So you created a table but forgot to add an email column, or you want to change
a column's data type. That's what ALTER is for — modifying an existing table.

### Add a new column
```sql
ALTER TABLE students ADD email VARCHAR(100);
```

### Modify an existing column
```sql
ALTER TABLE students MODIFY age SMALLINT;
```

### Rename a column
```sql
ALTER TABLE students RENAME COLUMN city TO hometown;
```

### Drop a column
```sql
ALTER TABLE students DROP COLUMN email;
```

> Think of ALTER like editing a form template — you're not filling it,
> you're changing what fields exist on it.

---
## ALTER — Editing What Already Exists

So you created a table but forgot to add an email column, or you want to change
a column's data type. That's what ALTER is for — modifying an existing table.

### Add a new column
```sql
ALTER TABLE students ADD email VARCHAR(100);
```

### Modify an existing column
```sql
ALTER TABLE students MODIFY age SMALLINT;
```

### Rename a column
```sql
ALTER TABLE students RENAME COLUMN city TO hometown;
```

### Drop a column
```sql
ALTER TABLE students DROP COLUMN email;
```

> Think of ALTER like editing a form template — you're not filling it,
> you're changing what fields exist on it.

---
## DROP — Deleting Everything, No Going Back

DROP deletes the **entire table** — the structure AND all the data inside it.
It's permanent. No undo button.

```sql
DROP TABLE students;
```

You can also drop an entire database:
```sql
DROP DATABASE college;
```

> ⚠️ Use DROP carefully. Once you drop a table, it's gone — data, structure, everything.

---

## TRUNCATE — Empty the Table, Keep the Structure

TRUNCATE removes **all the rows** from a table but keeps the table itself intact.
It's like emptying a box but keeping the box.

```sql
TRUNCATE TABLE students;
```

After this — the `students` table still exists, it's just empty.

---

## DROP vs TRUNCATE — The Difference That Always Gets Asked
| | TRUNCATE | DROP |
|---|---|---|
| Removes data? | ✅ Yes | ✅ Yes |
| Removes structure? | ❌ No | ✅ Yes |
| Can be rolled back? | ❌ No | ❌ No |
| Table still exists after? | ✅ Yes | ❌ No |

> Simple way to remember — **TRUNCATE empties the table, DROP kills the table.**

---

## All 4 Together — Quick Recap

```sql
-- Create a fresh table
CREATE TABLE students (id INT PRIMARY KEY, name VARCHAR(100), age INT);

-- Add a new column to it
ALTER TABLE students ADD email VARCHAR(100);

-- Empty all data but keep the table
TRUNCATE TABLE students;

-- Delete the table completely
DROP TABLE students;
```

---

## The Mental Model 🧠
CREATE  →  "Build the room"
ALTER   →  "Renovate the room"
TRUNCATE → "Clean out the room"
DROP    →  "Demolish the room"

---

> All 4 are DDL commands — they deal with **structure**, not data.
> None of them can be rolled back

