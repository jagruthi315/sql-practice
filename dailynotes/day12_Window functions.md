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
## ROW_NUMBER() — Unique Number for Each Row

Assigns a unique sequential number to each row.
Restarts from 1 for each partition.

```sql
SELECT name, city, salary,
    ROW_NUMBER() OVER (ORDER BY salary DESC) AS row_num
FROM employees;
```
name     salary   row_num

Sneha    70000    1

Riya     60000    2

Aman     50000    3

Karan    45000    4

Rahul    40000    5

### ROW_NUMBER with PARTITION BY

```sql
-- Rank employees within each city separately
SELECT name, city, salary,
    ROW_NUMBER() OVER (PARTITION BY city ORDER BY salary DESC) AS rank_in_city
FROM employees;
```
name    city      salary   rank_in_city

Aman    Delhi     50000    1

Karan   Delhi     45000    2

Riya    Mumbai    60000    1   ← restarts for Mumbai

Sneha   Mumbai    70000    ...

---

## RANK() — Rank with Gaps for Ties

Assigns rank to each row. If two rows tie, they get the
same rank and the next rank is skipped.

```sql
SELECT name, marks,
    RANK() OVER (ORDER BY marks DESC) AS rank
FROM students;
```
name    marks   rank

Aman    95      1

Priya   95      1     ← tie, both get rank 1

Karan   80      3     ← rank 2 is skipped!

Riya    75      4

---

## DENSE_RANK() — Rank without Gaps

Same as RANK but no gaps — next rank after a tie is
the very next number.

```sql
SELECT name, marks,
    DENSE_RANK() OVER (ORDER BY marks DESC) AS dense_rank
FROM students;
```
name    marks   dense_rank

Aman    95      1

Priya   95      1     ← tie, both get rank 1

Karan   80      2     ← no gap! next is 2 not 3

Riya    75      3

---
## RANK vs DENSE_RANK vs ROW_NUMBER
marks: 95, 95, 80, 75
ROW_NUMBER  → 1, 2, 3, 4   (always unique, no ties)

RANK        → 1, 1, 3, 4   (ties allowed, gaps exist)

DENSE_RANK  → 1, 1, 2, 3   (ties allowed, no gaps)

---

## SUM() OVER — Running Total / Partitioned Sum

```sql
-- Total salary per department added to each row
SELECT name, department, salary,
    SUM(salary) OVER (PARTITION BY department) AS dept_total
FROM employees;

-- Running total (cumulative sum)
SELECT name, salary,
    SUM(salary) OVER (ORDER BY name) AS running_total
FROM employees;
```

---

## AVG() OVER — Running/Partitioned Average

```sql
SELECT name, city, salary,
    AVG(salary) OVER (PARTITION BY city) AS avg_city_salary
FROM employees;
```

Each row shows the average salary of its city —
without collapsing rows like GROUP BY would.

## LAG() — Access Previous Row's Value

LAG lets you look at the value from the previous row.
Very useful for comparing current vs previous.

```sql
SELECT name, salary,
    LAG(salary) OVER (ORDER BY id) AS prev_salary
FROM employees;
```
name    salary   prev_salary

Aman    50000    NULL        ← no previous row

Riya    60000    50000

Karan   45000    60000

Sneha   70000    45000

---

## LEAD() — Access Next Row's Value

Opposite of LAG — looks at the next row's value.

```sql
SELECT name, salary,
    LEAD(salary) OVER (ORDER BY id) AS next_salary
FROM employees;
```
name    salary   next_salary

Aman    50000    60000

Riya    60000    45000

Karan   45000    70000

Sneha   70000    NULL        ← no next row

---

## NTILE(n) — Divide Rows into Buckets

Divides rows into n equal groups and assigns a bucket number.

```sql
-- Divide employees into 4 salary quartiles
SELECT name, salary,
    NTILE(4) OVER (ORDER BY salary DESC) AS quartile
FROM employees;
```

---

## All Window Functions — Quick Reference Table

| Function | What it does |
|----------|--------------|
| `ROW_NUMBER()` | Unique number per row, no ties |
| `RANK()` | Rank with gaps for ties |
| `DENSE_RANK()` | Rank without gaps for ties |
| `SUM() OVER` | Running or partitioned sum |
| `AVG() OVER` | Running or partitioned average |
| `MIN() OVER` | Min value in partition |
| `MAX() OVER` | Max value in partition |
| `LAG()` | Value from previous row |
| `LEAD()` | Value from next row |
| `NTILE(n)` | Divide rows into n buckets |

---

## Window Functions vs GROUP BY

| | GROUP BY | Window Function |
|--|----------|----------------|
| Collapses rows? | ✅ Yes | ❌ No |
| Keeps original rows? | ❌ No | ✅ Yes |
| Can see individual rows? | ❌ No | ✅ Yes |
| Use with aggregate? | ✅ Yes | ✅ Yes |

---

## 🧠 Memory Tricks
OVER()         → "this is a window function"

PARTITION BY   → "group by, but don't collapse"

ORDER BY       → "order within the window"
ROW_NUMBER → always unique (1,2,3,4)

RANK       → gaps on ties (1,1,3,4)

DENSE_RANK → no gaps on ties (1,1,2,3)
LAG  → look BACK  (previous row)

LEAD → look AHEAD (next row)

---

## ⚡ Quick Reference

```sql
-- Row number
SELECT name, ROW_NUMBER() OVER (ORDER BY salary DESC) FROM employees;

-- Rank with gaps
SELECT name, RANK() OVER (ORDER BY marks DESC) FROM students;

-- Rank without gaps
SELECT name, DENSE_RANK() OVER (ORDER BY marks DESC) FROM students;

-- Partition sum
SELECT name, SUM(salary) OVER (PARTITION BY city) FROM employees;

-- Running total
SELECT name, SUM(salary) OVER (ORDER BY id) FROM employees;

-- Previous row
SELECT name, LAG(salary) OVER (ORDER BY id) FROM employees;

-- Next row
SELECT name, LEAD(salary) OVER (ORDER BY id) FROM employees;
```

