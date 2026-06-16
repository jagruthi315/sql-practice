# Day 10 --> JOINs


JOINs are how you combine data from multiple tables.
In real life, data is never stored in one table —
customer info is separate, orders are separate, departments are separate.
JOINs bring them together.

---

## The Big Picture — Two Ways to Combine Tables
Combine two tables?

|

|

|           |

ROWS        COLUMNS

|           |

SET OPS     JOINs

(UNION,     (INNER, LEFT,

INTERSECT,   RIGHT, FULL)

EXCEPT)

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
