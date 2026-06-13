# Day 9 --> Subqueries


---

## What is a Subquery?

A subquery is a query **nested inside another SQL query**.
It can be used inside SELECT, FROM, or WHERE clauses.

> Important rule: the **innermost query runs first**,
> then the outer query uses that result.

---

## A Real Example — Why Subqueries Exist

**Question:** "Show all employees whose salary is more than
the average salary of all employees."

### ❌ This does NOT work:

```sql
SELECT * FROM employees WHERE employee_salary > avg(employee_salary);
-- Error Code: 1111. Invalid use of group function
```

You can't directly compare a column to an aggregate function
in the same WHERE clause — SQL doesn't know how to do that
in one step.

### ✅ This is the fix — a subquery:

```sql
SELECT * FROM employees
WHERE employee_salary > (SELECT AVG(employee_salary) FROM employees);
```

**What happens step by step:**
1. Inner query runs first:
```sql
   SELECT AVG(employee_salary) FROM employees;
   -- Returns: 46826.0870
```
2. Outer query then becomes:
```sql
   SELECT * FROM employees WHERE employee_salary > 46826.0870;
   -- Returns 12 rows
```

> So the subquery basically gives the outer query a value to compare with.

---

