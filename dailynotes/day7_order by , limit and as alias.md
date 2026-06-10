# Day 7 --> ORDER BY, LIMIT & AS / Alias

## AS — Alias (Rename Temporarily)

AS gives a temporary name to a column or table in the output.
It does NOT change anything in the actual database — just makes
the result cleaner and easier to read.

### Column Alias

```sql
-- Without AS — messy output
SELECT AVG(marks) FROM students;
-- column shows as: AVG(marks)

-- With AS — clean output
SELECT AVG(marks) AS average_marks FROM students;
-- column shows as: average_marks
```

### Rename Columns

```sql
SELECT name AS student_name FROM students;

-- Multiple columns
SELECT name AS student_name, marks AS student_marks FROM students;
```

### AS with Calculations

```sql
SELECT marks + 5 AS updated_marks FROM students;
SELECT salary * 12 AS yearly_salary FROM employees;
```

### Table Alias — Important for JOINs

```sql
-- Without alias — long and repetitive
SELECT students.name, marks.marks
FROM students JOIN marks ON students.id = marks.student_id;

-- With alias — short and clean
SELECT s.name, m.marks
FROM students AS s JOIN marks AS m ON s.id = m.student_id;
```

> AS is temporary — only exists in that query's output.
> You can skip writing AS and just put the alias directly,
> but writing AS is cleaner and recommended.

### Quick Reference

| Use | Example |
|-----|---------|
| Column alias | `marks AS student_marks` |
| Aggregate alias | `AVG(marks) AS avg_marks` |
| Table alias | `students AS s` |
| Calculated column | `salary*12 AS yearly_salary` |

---

## ORDER BY — Sort Your Results

ORDER BY sorts the result of your query.
By default it sorts in ascending order (smallest to largest).

```sql
-- Ascending (default)
SELECT * FROM students ORDER BY marks;
SELECT * FROM students ORDER BY marks ASC;

-- Descending (largest first)
SELECT * FROM students ORDER BY marks DESC;
```

### Order by Multiple Columns

```sql
-- Sort by city first, then by salary within each city
SELECT name, city, salary
FROM employees
ORDER BY city ASC, salary DESC;
```

How it works:
- First sorts everyone by city A → Z
- Then within each city, sorts by salary highest → lowest

### ORDER BY with Column Number

```sql
-- Instead of column name, use its position
SELECT name, marks FROM students ORDER BY 2 DESC;


## LIMIT — Control How Many Rows You Get

LIMIT restricts how many rows are returned.
Very useful for top N queries.

```sql
-- Get only 5 rows
SELECT * FROM students LIMIT 5;

-- Top 3 highest marks
SELECT name, marks FROM students
ORDER BY marks DESC
LIMIT 3;
```

### OFFSET — Skip Rows (Pagination)

```sql
-- Skip first 5 rows, then get next 5
SELECT * FROM students LIMIT 5 OFFSET 5;

-- Page 1: LIMIT 5 OFFSET 0
-- Page 2: LIMIT 5 OFFSET 5
-- Page 3: LIMIT 5 OFFSET 10
```

> OFFSET is how apps show "page 1, page 2, page 3" of results.

### Nested ORDER BY

```sql
-- Real example: top 5 employees per city by salary
SELECT name, city, salary
FROM employees
ORDER BY city ASC, salary DESC
LIMIT 5;
```

---

## Putting It All Together

```sql
SELECT
    name AS student_name,
    marks AS total_marks
FROM students
WHERE marks > 50
ORDER BY marks DESC
LIMIT 10;
```

What this does step by step:
1. FROM students — go to students table
2. WHERE marks > 50 — keep only students with marks above 50
3. ORDER BY marks DESC — sort highest marks first
4. LIMIT 10 — show only top 10
5. SELECT + AS — show name and marks with clean column names

---

## 🧠 Memory Tricks
AS      → "call it this name instead"
ORDER BY → "sort it this way"
LIMIT   → "show me only this many"
OFFSET  → "skip this many first"
ASC  = A to Z, 1 to 9  (default)
DESC = Z to A, 9 to 1

---

## ⚡ Quick Reference

```sql
-- Alias
SELECT AVG(salary) AS avg_salary FROM employees;

-- Order ascending
SELECT * FROM students ORDER BY marks ASC;

-- Order descending
SELECT * FROM students ORDER BY marks DESC;

-- Multiple column sort
SELECT * FROM employees ORDER BY city ASC, salary DESC;

-- Limit results
SELECT * FROM students ORDER BY marks DESC LIMIT 5;

-- Pagination
SELECT * FROM students LIMIT 10 OFFSET 20;
```


-- 2 means second column = marks
```

> Not recommended for real code but sometimes seen in HackerRank.

---
