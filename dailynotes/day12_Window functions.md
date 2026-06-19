# Day 12--> Window Functions


Window functions are one of the most powerful and most asked
topics in SQL interviews. Today we level up! 🚀

---

## What are Window Functions?

A window function performs a calculation across a set of rows
**related to the current row** — without collapsing them into
a single result like aggregate functions do.

Think of it like this:
- `GROUP BY + SUM` → many rows become ONE row (collapsed)
- `Window SUM` → many rows stay as they are, but each row
  gets the sum value added to it (not collapsed)

```sql
-- Aggregate (collapses rows)
SELECT city, SUM(salary) FROM employees GROUP BY city;
-- Output: 3 rows (one per city)

-- Window Function (keeps all rows)
SELECT name, city, salary,
    SUM(salary) OVER (PARTITION BY city) AS city_total
FROM employees;
-- Output: all rows, each with city total added
```

---

## Syntax — General Structure

```sql
function_name() OVER (
    PARTITION BY column   -- like GROUP BY for windows
    ORDER BY column       -- order within each partition
)
```

- `PARTITION BY` → divides rows into groups (like GROUP BY)
- `ORDER BY` → orders rows within each partition
- Both are optional depending on what you need

---

