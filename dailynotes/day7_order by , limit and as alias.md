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
-- 2 means second column = marks
```

> Not recommended for real code but sometimes seen in HackerRank.

---
