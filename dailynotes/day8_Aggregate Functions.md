# Day 8 --> Aggregate Functions


## What are Aggregate Functions?

Aggregate functions perform a calculation on a set of values
and return a **single result**. They help summarize data —
totals, averages, counts, etc.

**Real life example:**
You're an HR Manager with a list of 1000 employees in Excel.
You want to know:

- How many total employees? → `COUNT()`
- What's the average salary in the company? → `AVG()`
- What's the highest salary? → `MAX()`

In SQL, aggregate functions answer all these in just one line.

---

## Common Aggregate Functions

| Function | What it does |
|----------|--------------|
| `COUNT()` | Counts number of rows |
| `SUM()` | Adds all values |
| `AVG()` | Calculates average value |
| `MIN()` / `MAX()` | Finds lowest / highest value |

---

## COUNT() — Count Rows

```sql
-- How many customers are there?
SELECT COUNT(customer_id) FROM customer;
-- Output: 24
```

> ⚠️ Note: `COUNT(customer_id)` vs `COUNT(customer_name)` can
> give different results if some names are NULL — COUNT skips
> NULL values for that column.

```sql
SELECT COUNT(customer_name) FROM customer;
-- Output: 23 (one row had a NULL name, so it's skipped)
```

> Use `COUNT(*)` to count ALL rows regardless of NULLs.

---

## MAX() — Highest Value

```sql
SELECT MAX(employee_salary) FROM employees;
-- Output: 62000
```

---

## MIN() — Lowest Value

```sql
SELECT MIN(employee_salary) FROM employees;
-- Output: 35000
```

---

## AVG() — Average Value

```sql
SELECT AVG(employee_salary) FROM employees;
-- Output: 46826.0870
```

> ⚠️ Common mistake: `AVG()(employee_salary)` — extra brackets
> cause a syntax error (Error Code: 1064).
> Correct syntax: `AVG(employee_salary)`

---

## SUM() — Total of All Values

```sql
SELECT SUM(employee_salary) FROM employees;
-- Adds up all salaries
```

---

## Bonus — Pattern Matching Recap (used alongside aggregates)

```sql
-- Names where the 2nd character is 'a'
-- _ means exactly one character, % means any number after
SELECT employee_name FROM employees
WHERE employee_name LIKE '_a%';
-- Matches: Aman, Karan, Varun... (2nd letter = a)
```

```sql
-- Employees from Delhi or Mumbai
SELECT * FROM employees
WHERE employee_city IN ('Delhi', 'Mumbai');
```

---

## Aggregate Functions + GROUP BY (connecting to Day 6)

Aggregate functions become even more powerful when combined
with GROUP BY:

```sql
-- Average salary per city
SELECT employee_city, AVG(employee_salary)
FROM employees
GROUP BY employee_city;

-- Highest salary per city, only show cities with > 2 employees
SELECT employee_city, MAX(employee_salary)
FROM employees
GROUP BY employee_city
HAVING COUNT(employee_id) > 2;
```

---

## 🧠 Memory Tricks
COUNT() → "how many?"

SUM()   → "total of all"

AVG()   → "average"

MIN()   → "smallest"

MAX()   → "biggest"
All aggregate functions → many values IN, one value OUT

---

## ⚡ Quick Reference

```sql
SELECT COUNT(*) FROM table;          -- total rows
SELECT COUNT(column) FROM table;     -- non-null values only
SELECT SUM(column) FROM table;       -- total sum
SELECT AVG(column) FROM table;       -- average
SELECT MIN(column) FROM table;       -- smallest value
SELECT MAX(column) FROM table;       -- largest value

-- with GROUP BY
SELECT category, COUNT(*) FROM table GROUP BY category;
```

---

## ⚠️ Common Mistakes to Avoid

- `AVG()(column)` → wrong, extra brackets cause error
- `COUNT(column)` skips NULL values, `COUNT(*)` doesn't
- Aggregate functions need `GROUP BY` if mixed with non-aggregate columns

---


