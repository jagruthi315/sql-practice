# Day 13 --> CTEs (Common Table Expressions)


CTEs make complex queries readable. Once you get comfortable
with these, writing multi-step SQL logic becomes so much easier.

---

## What is a CTE?

A CTE is a **temporary named result set** defined using `WITH`
that exists **only within that query**. It's mainly used to
break down complex queries into smaller, readable steps.

> Important: A CTE doesn't give memory/storage to the table
> being formed — it exists only temporarily, just long enough
> to help you reach your end goal. It's used when you need
> specific values from a table without wasting memory storing
> the whole thing — you build it, then filter it, all in one go.

---

## Syntax

```sql
WITH cte_name AS (
    SELECT ...
)
SELECT * FROM cte_name;
```

> Everything from `WITH` till the semicolon `;` is **one single query**.
> It runs together, not separately. The CTE only exists for
> the duration of that query.

---

## Real Example — Window Function + CTE

**Goal:** Find the top-ranked student in each class based on marks.

```sql
WITH a AS (
    SELECT student_id, name, class, marks,
        DENSE_RANK() OVER (PARTITION BY class ORDER BY marks DESC) AS ranks_students
    FROM studentsag
)
SELECT * FROM a WHERE ranks_students = 1;
```

**What's happening:**
1. The CTE `a` calculates a `DENSE_RANK()` for each student,
   partitioned by class, ordered by marks (highest first)
2. The outer query then filters the CTE to only show rank 1
   (the top student per class)

Output:
| student_id | name | class | marks | ranks_students |
|-----------|------|-------|-------|----------------|
| 1 | Aman | 10A | 95 | 1 |
| 3 | Rohit | 10A | 95 | 1 |
| 1 | Riya | 10B | 95 | 1 |
| 3 | Jiya | 10B | 95 | 1 |

> Two students tied for rank 1 in each class (because of
> DENSE_RANK on equal marks) — both show up correctly.

---

## Important Rule — CASE Inside CTE

You **cannot directly filter on a column created by CASE**
in the same query level. If you want to use that calculated
column (like a CASE result) in a WHERE clause, you must put
the CASE statement **inside the CTE** first, then filter on
it in the outer query.

```sql
-- ✅ CASE defined inside the CTE
WITH a AS (
    SELECT *,
        CASE
            WHEN revenue >= 60000 AND revenue < 90000 THEN 'low'
            WHEN revenue >= 90000 AND revenue < 120000 THEN 'mid'
            ELSE 'high'
        END AS revenue_ranks,
        DENSE_RANK() OVER (PARTITION BY region ORDER BY revenue DESC) AS rank_val
    FROM sales2
)
SELECT * FROM a WHERE revenue_ranks = 'high';
```

Output:
| emp_id | emp_name | region | revenue | revenue_ranks | rank_val |
|--------|----------|--------|---------|---------------|---------|
| 1 | Aman | North | 120000 | high | 1 |
| 3 | Rohit | South | 150000 | high | 1 |
| 4 | Meera | South | 150000 | high | 1 |

> 📌 Mistake to watch out for: if you want the **highest revenue
> per region**, use `WHERE rank_val = 1` instead of just
> showing high revenue with a LIMIT — LIMIT only cuts off rows
> from the whole result, it doesn't respect "per region" grouping.

```sql
-- ✅ Correct way to get top revenue PER region
SELECT * FROM a WHERE rank_val = 1;
```

---

## When to Use a CTE

> Whenever you have a complex query, AND you know that after
> defining/calculating something, you need to apply filters
> on top of it — that's when you reach for a CTE.

Common situations:
- Calculating a window function (RANK, DENSE_RANK) and then filtering on it
- Using a CASE statement and then filtering on the resulting category
- Breaking a long nested subquery into clean readable steps

---

## CTE vs Subquery

| | CTE | Subquery |
|--|-----|----------|
| Readability | ✅ Cleaner, step-by-step | Can get messy when nested |
| Reusability | ✅ Can reference multiple times in same query | One-time use |
| Best for | Complex multi-step logic | Simple one-off comparisons |
| Memory | Temporary, no storage | Temporary, no storage |

---

## Multiple CTEs in One Query

```sql
WITH
    high_revenue AS (
        SELECT * FROM sales WHERE revenue > 100000
    ),
    region_summary AS (
        SELECT region, COUNT(*) AS total FROM high_revenue GROUP BY region
    )
SELECT * FROM region_summary;
```

---

## 🧠 Memory Tricks
CTE = "a temporary helper table that disappears after the query"

WITH ... AS (...) → defines it

SELECT * FROM cte_name → uses it
Rule: Need to filter on a calculated column (CASE/window function)?

→ Put the calculation inside the CTE, filter in the outer query

---

## ⚡ Quick Reference

```sql
-- Basic CTE
WITH cte_name AS (
    SELECT * FROM table_name WHERE condition
)
SELECT * FROM cte_name;

-- CTE with window function, filtered outside
WITH ranked AS (
    SELECT *, RANK() OVER (PARTITION BY col ORDER BY col2 DESC) AS rnk
    FROM table_name
)
SELECT * FROM ranked WHERE rnk = 1;

-- CTE with CASE, filtered outside
WITH categorized AS (
    SELECT *,
        CASE WHEN x > 100 THEN 'high' ELSE 'low' END AS category
    FROM table_name
)
SELECT * FROM categorized WHERE category = 'high';
```

---
