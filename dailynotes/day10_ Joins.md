# Day 10 --> JOINs


JOINs are how you combine data from multiple tables.
In real life, data is never stored in one table —
customer info is separate, orders are separate, departments are separate.
JOINs bring them together.

---

## The Big Picture — Two Ways to Combine Tables

When combining two tables you have two options:

| | SET Operators | JOINs |
|--|--------------|-------|
| Combines | Rows (vertically) | Columns (horizontally) |
| Examples | UNION, INTERSECT, EXCEPT | INNER, LEFT, RIGHT, FULL |
| Needs | Same number of columns | A key column |

- Want to **stack rows**? → SET Operators
- Want to **add columns**? → JOINs
- **SET Operators** → stack tables **vertically** (add rows) — need same columns
- **JOINs** → expand tables **horizontally** (add columns) — need a key column

---

## Why Do We Need JOINs?

1. **Recombine Data** — combine split data into one big picture table
2. **Data Enrichment** — get extra info from another table
3. **Check Existence** — check if data exists or doesn't exist in another table
4. **Filtering** — filter based on conditions across tables

---

## Key Rule Before Joining

> To JOIN two tables, you need a **common key column**
> — a column that has the same data in both tables.
> The column names can be different, but the data must match.
customers table          orders table

id | first_name          order_id | customer_id | sales

1  | Maria               1001     | 1           | 35

2  | John                1002     | 2           | 15

Here `customers.id` and `orders.customer_id` have matching data
— this is the key column we JOIN on.

---
NION, INTERSECT, EXCEPT)


## JOIN Syntax — General Structure

```sql
SELECT *
FROM A
[TYPE] JOIN B
ON A.key = B.key;
```

> Default JOIN type is INNER JOIN if you just write JOIN.

---

## No JOIN — Two Separate Queries

When you don't need to combine tables at all.

```sql
-- Two separate results, no combining needed
SELECT * FROM customers;
SELECT * FROM orders;
```

---

## INNER JOIN — Only Matching Rows

Returns only rows that have a match in BOTH tables.
If a row exists in A but not in B — it's excluded.
A ∩ B = only common/matching data

```sql
-- Get all customers who have placed an order
SELECT *
FROM customers
INNER JOIN orders
ON id = customer_id;
```

Output — only customers who have orders:
| id | first_name | country | score | order_id | customer_id | sales |
|----|-----------|---------|-------|----------|-------------|-------|
| 1 | Maria | Germany | 350 | 1001 | 1 | 35 |
| 2 | John | USA | 900 | 1002 | 2 | 15 |
| 3 | Georg | UK | 750 | 1003 | 3 | 20 |

> ⚠️ In INNER JOIN, order of tables doesn't matter —
> A JOIN B = B JOIN A (same result)

---

## Column Ambiguity — Important!

When two tables have columns with the same name, SQL gets confused.

```sql
-- ❌ Column ambiguity — which 'id' do you mean?
SELECT id, first_name, id, sales
FROM customers
INNER JOIN orders ON id = customer_id;
```

### Fix — Use table name before column:

```sql
-- ✅ Specify which table each column comes from
SELECT customers.id, customers.first_name, orders.order_id, orders.sales
FROM customers
INNER JOIN orders ON customers.id = orders.customer_id;
```

### Even Better — Use Aliases:

```sql
-- ✅ Clean and short using aliases
SELECT c.id, c.first_name, o.order_id, o.sales
FROM customers AS c
INNER JOIN orders AS o
ON c.id = o.customer_id;
```

---

## LEFT JOIN — All of Left + Matching from Right

Returns ALL rows from the left table (A), and only matching
rows from the right table (B). Non-matching right side = NULL.
All of A + matching part of B

```sql
SELECT c.id, c.first_name, o.order_id, o.sales
FROM customers AS c
LEFT JOIN orders AS o
ON c.id = o.customer_id;
```

Customers without orders still appear — their order columns show NULL.

---

## RIGHT JOIN — All of Right + Matching from Left

Opposite of LEFT JOIN. Returns ALL rows from the right table (B),
only matching from left (A).

```sql
SELECT e.emp_name, d.dept_name
FROM employees AS e
RIGHT JOIN departments AS d
ON e.dept_id = d.dept_id;
```

All departments show — even if no employee is assigned to them.

---

## FULL JOIN — Everything from Both Tables

Returns ALL rows from both tables.
Non-matching rows show NULL on the missing side.

```sql
SELECT *
FROM customers AS c
FULL JOIN orders AS o
ON c.id = o.customer_id;
```

> MySQL doesn't support FULL JOIN directly —
> use UNION of LEFT JOIN and RIGHT JOIN instead.

---

## JOIN Types — Visual Summary
NO JOIN     → A    B       two separate results

INNER JOIN  → A ∩ B        only matching rows

LEFT JOIN   → A + (A ∩ B)  all left + matched right

RIGHT JOIN  → B + (A ∩ B)  all right + matched left

FULL JOIN   → A ∪ B        everything from both

---

## Advanced JOINs (Quick Overview)

| Join | Returns |
|------|---------|
| Left Anti Join | Only rows in A that have NO match in B |
| Right Anti Join | Only rows in B that have NO match in A |
| Full Anti Join | Rows from both that have NO match in the other |
| Cross Join | Every combination of A and B (cartesian product) |

---

## SET Operators vs JOINs — Final Difference

| | SET Operators | JOINs |
|--|--------------|-------|
| Combines | Rows (vertical) | Columns (horizontal) |
| Needs | Same number of columns | Key column |
| Examples | UNION, INTERSECT, EXCEPT | INNER, LEFT, RIGHT, FULL |

---

## 🧠 Memory Tricks
INNER JOIN  → "only where they match" (strictest)

LEFT JOIN   → "keep everything from left, match what you can"

RIGHT JOIN  → "keep everything from right, match what you can"

FULL JOIN   → "keep everything from both"
For LEFT and RIGHT JOIN — order of tables matters!

For INNER JOIN — order doesn't matter

---

## ⚡ Quick Reference

```sql
-- INNER JOIN
SELECT c.name, o.sales
FROM customers c
INNER JOIN orders o ON c.id = o.customer_id;

-- LEFT JOIN
SELECT c.name, o.sales
FROM customers c
LEFT JOIN orders o ON c.id = o.customer_id;

-- RIGHT JOIN
SELECT e.emp_name, d.dept_name
FROM employees e
RIGHT JOIN departments d ON e.dept_id = d.dept_id;
```


