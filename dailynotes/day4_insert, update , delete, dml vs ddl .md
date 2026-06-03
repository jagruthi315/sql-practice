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


```

---

## 🧠 Memory Tricks
