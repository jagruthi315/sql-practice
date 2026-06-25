# Day 16 --> Stored Procedures

Stored Procedures are saved collections of SQL statements stored inside the database. Instead of writing the same SQL queries repeatedly, you can save them once and execute them whenever needed.

Think of a Stored Procedure as a function in programming that lives inside the database.

---

# What is a Stored Procedure?

A Stored Procedure is a pre-written set of SQL statements that can be executed whenever required.

Instead of repeatedly writing:

```sql
SELECT * FROM Students;
```

you can create a procedure once and call it whenever needed.

---

# Real-Life Analogy

Imagine every day you perform these tasks:

1. Find all orders
2. Calculate total sales
3. Generate a report

Instead of manually doing all three steps every day, you create a button:

```text
GenerateSalesReport()
```

Click the button and everything runs automatically.

That's exactly how a Stored Procedure works.

---

# Why Do We Use Stored Procedures?

Stored Procedures are useful because they:

* Reduce repeated code
* Improve reusability
* Improve security
* Can improve performance
* Allow business logic inside the database

---

# Basic Syntax

```sql
CREATE PROCEDURE procedure_name()
BEGIN
    SQL statements;
END;
```

Example:

```sql
CREATE PROCEDURE GetStudents()
BEGIN
    SELECT *
    FROM Students;
END;
```

Execute:

```sql
CALL GetStudents();
```

Output:

| id | name  |
| -- | ----- |
| 1  | Rahul |
| 2  | Priya |

---

# Reusability

Without a procedure:

```sql
SELECT * FROM Students;
```

You may write the same query repeatedly.

With a procedure:

```sql
CALL GetStudents();
```

The SQL is written once and reused whenever needed.

---

# Reduce Repeated Code

Suppose every month you run:

```sql
SELECT *
FROM Orders
WHERE order_date >= '2025-01-01';
```

Instead of rewriting this query repeatedly, save it inside a procedure.

---

# Performance Benefits

Stored Procedures are compiled and stored by the database.

Because the database already knows the query structure, execution can sometimes be faster.

### Interview Answer

Stored Procedures can improve performance by reducing query parsing and optimization overhead.

---

# Security Benefits

Users can be given permission to execute a procedure without giving direct access to underlying tables.

Example:

```sql
CALL GetEmployees();
```

Allowed.

But:

```sql
SELECT * FROM Employees;
```

May not be allowed.

This helps protect sensitive data.

---

# Stored Procedure with Parameters

Parameters make procedures much more useful.

Suppose the Students table contains:

| id | name  | marks |
| -- | ----- | ----- |
| 1  | Rahul | 85    |
| 2  | Priya | 70    |
| 3  | Rohan | 92    |

Create procedure:

```sql
CREATE PROCEDURE GetStudent(IN student_id INT)
BEGIN
    SELECT *
    FROM Students
    WHERE id = student_id;
END;
```

Execute:

```sql
CALL GetStudent(2);
```

Output:

| id | name  | marks |
| -- | ----- | ----- |
| 2  | Priya | 70    |

---

# Procedure with Multiple Parameters

```sql
CREATE PROCEDURE StudentsAboveMarks(IN min_marks INT)
BEGIN
    SELECT *
    FROM Students
    WHERE marks > min_marks;
END;
```

Execute:

```sql
CALL StudentsAboveMarks(80);
```

Returns all students scoring above 80 marks.

---

# Using Variables

Stored Procedures can store values inside variables.

Example:

```sql
CREATE PROCEDURE Demo()
BEGIN
    DECLARE total INT;

    SELECT COUNT(*)
    INTO total
    FROM Students;

    SELECT total;
END;
```

---

# Understanding the Example

## Step 1: Create Variable

```sql
DECLARE total INT;
```

Creates a variable named `total`.

Think:

```python
total = 0
```

---

## Step 2: Store Query Result

```sql
SELECT COUNT(*)
INTO total
FROM Students;
```

Suppose Students contains:

| id | name   |
| -- | ------ |
| 1  | Rahul  |
| 2  | Priya  |
| 3  | Rohan  |
| 4  | Ananya |

COUNT(*) returns:

```text
4
```

The result is stored in:

```text
total = 4
```

Think of:

```sql
INTO total
```

as:

```python
total =
```

---

## Step 3: Display Variable

```sql
SELECT total;
```

Output:

```text
4
```

---

# Visual Flow

Students Table

```text
4 Rows
```

↓

```sql
SELECT COUNT(*)
```

↓

```text
4
```

↓

```sql
INTO total
```

↓

```text
total = 4
```

↓

```sql
SELECT total;
```

↓

```text
4
```

---
# IF-ELSE in Stored Procedures

Stored Procedures can contain conditional logic.

```sql
CREATE PROCEDURE CheckMarks(IN marks INT)
BEGIN

    IF marks >= 80 THEN
        SELECT 'Excellent';

    ELSE
        SELECT 'Average';

    END IF;

END;
```

Execute:

```sql
CALL CheckMarks(90);
```

Output:

```text
Excellent
```

---

# Loops in Stored Procedures

Stored Procedures can also use loops.

Example syntax:

```sql
WHILE condition DO
    statements;
END WHILE;
```

Loops are less common in Data Analyst work but are useful to know.

---

# Stored Procedure vs View

| Feature    | View              | Stored Procedure        |
| ---------- | ----------------- | ----------------------- |
| Type       | Virtual Table     | Saved Program           |
| Contains   | Usually One Query | Multiple SQL Statements |
| Parameters | No                | Yes                     |
| Purpose    | Display Data      | Perform Operations      |
| Execution  | SELECT            | CALL / EXEC             |

## View Example

```sql
CREATE VIEW TopStudents AS
SELECT *
FROM Students
WHERE marks > 80;
```

Use:

```sql
SELECT * FROM TopStudents;
```

## Procedure Example

```sql
CREATE PROCEDURE GetTopStudents()
BEGIN
    SELECT *
    FROM Students
    WHERE marks > 80;
END;
```

Use:

```sql
CALL GetTopStudents();
```

---

# Stored Procedure vs Function

Many beginners confuse these.

## Function

Returns a single value.

Example:

```sql
GetTax(10000)
```

Returns:

```text
1800
```

## Stored Procedure

Can:

* Return result sets
* Insert data
* Update data
* Delete data
* Perform multiple operations

Stored Procedures are generally more powerful.

---

# Common Interview Questions

## What is a Stored Procedure?

A precompiled collection of SQL statements stored in the database that can be executed repeatedly.

## Advantages?

* Reusability
* Better performance
* Security
* Less repeated code

## Can Stored Procedures Accept Parameters?

✅ Yes

Example:

```sql
CALL GetStudent(5);
```

## Difference Between Procedure and Function?

### Procedure

* Performs multiple operations
* Can return result sets

### Function

* Returns a single value

---

# Quick Reference

```sql
-- Create Procedure
CREATE PROCEDURE procedure_name()
BEGIN
    SQL statements;
END;

-- Execute Procedure
CALL procedure_name();

-- Procedure with Parameter
CREATE PROCEDURE GetStudent(IN student_id INT)
BEGIN
    SELECT *
    FROM Students
    WHERE id = student_id;
END;

CALL GetStudent(2);
```

---

# Memory Tricks

Stored Procedure = Saved Program

View = Saved Query

Function = Returns One Value

Think:

* View → Display Data
* Procedure → Perform Tasks
* Function → Return Value

---

# Small Note for DA Learning

For a Data Analyst, you may not create Stored Procedures every day, but you should understand:

* How automated reports are generated
* How business logic is stored in databases
* Why analysts sometimes receive data from procedures rather than tables
* Basic procedure syntax for interviews

Stored Procedures are commonly asked in SQL interviews because they combine SQL knowledge with database concepts such as performance, security, automation, and reusability.

---

# SQL Series Complete 🎉

Congratulations on completing this SQL learning journey.

Topics Covered:

* SELECT
* WHERE
* ORDER BY
* GROUP BY
* HAVING
* JOINS
* Subqueries
* Window Functions
* CTEs
* Indexes
* Views
* Stored Procedures

Next Steps for a Data Analyst:

1. Advanced Excel
2. Power BI
3. Statistics
4. Python (Pandas, NumPy)
5. Data Visualization
6. SQL Projects
7. End-to-End Portfolio Projects

Remember:

> SQL helps you get data.
>
> Analysis helps you create insights.
>
> Business understanding helps you create impact.


