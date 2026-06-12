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

---


