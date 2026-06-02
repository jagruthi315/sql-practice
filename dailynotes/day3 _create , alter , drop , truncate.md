#Day 3 --> CREATE, ALTER, DROP, TRUNCATE

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
