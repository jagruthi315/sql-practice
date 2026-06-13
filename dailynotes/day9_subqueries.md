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


## When To Use a Subquery — Simple Signal

If the question sounds like any of these, use a subquery:

- "greater than **average**"
- "equal to **maximum/minimum**"
- "**in the list of** ..."
- "**exists in** another table"

---

## Common Situations (with examples)

### 1. Compare with an aggregate value

"Employees with salary greater than average"

```sql
SELECT * FROM employees
WHERE salary > (
    SELECT AVG(salary) FROM employees
);
```
> You cannot do this without a subquery.

---

### 2. Match values from another table

"Employees whose department is IT"

```sql
SELECT name FROM employees
WHERE dept_id IN (
    SELECT dept_id FROM departments WHERE dept_name = 'IT'
);
```

---

### 3. Find max/min related data

"Employee with the highest salary"

```sql
SELECT * FROM employees
WHERE salary = (
    SELECT MAX(salary) FROM employees
);
```

---

### 4. Check existence — EXISTS

```sql
SELECT name FROM employees e
WHERE EXISTS (
    SELECT 1 FROM departments d
    WHERE e.dept_id = d.dept_id
);
```

---

## When NOT to Use a Subquery

Don't use a subquery if a simple query works fine.

```sql
-- No subquery needed here
SELECT * FROM employees WHERE salary > 40000;
```

> Only use subqueries when you genuinely need a value
> computed from another query.

---

## Can We Write a Query Inside a Subquery?

✅ **YES** — subqueries can be nested multiple levels deep.

```sql
-- Subquery inside a subquery
SELECT name FROM employees
WHERE salary > (
    SELECT AVG(salary) FROM employees
    WHERE dept_id IN (
        SELECT dept_id FROM departments WHERE location = 'Delhi'
    )
);
```

**Levels of nesting:**
Main Query

↓

Subquery

↓

Subquery inside subquery

> SQL supports multiple levels of nesting,
> but keep it simple in exams/interviews.

---


