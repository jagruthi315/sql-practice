# Day 17 --> NULL Handling (COALESCE, ISNULL, IS NULL & IS NOT NULL)

NULL handling is one of the most important concepts in SQL because NULL behaves differently from normal values. It is frequently asked in interviews and is commonly used in real-world data analysis.

---

# What is NULL?

`NULL` represents a missing, unknown, or unavailable value.

It is **not**:

* ❌ 0
* ❌ Empty String (`''`)
* ❌ False

It **is**:

* ✅ Missing or Unknown Value

Example:

| id | name  | phone      |
| -- | ----- | ---------- |
| 1  | Rahul | 9876543210 |
| 2  | Priya | NULL       |
| 3  | Rohan | 8765432101 |

Here, Priya's phone number is unknown, so it is stored as `NULL`.

---

# Why is NULL Important?

NULL behaves differently from normal values.

Suppose you run:

```sql
SELECT phone + 10
FROM Students;
```

Output:

| phone      |
| ---------- |
| 9876543220 |
| NULL       |
| 8765432111 |

For Priya:

```text
NULL + 10 = NULL
```

Any arithmetic operation involving `NULL` usually returns `NULL`.

---

# COALESCE()

## Definition

`COALESCE()` returns the **first non-NULL value** from a list of values.

### Syntax

```sql
COALESCE(value1, value2, value3, ...)
```

SQL checks the values from **left to right** and returns the first value that is **not NULL**.

---

# Example 1

```sql
SELECT COALESCE(NULL, NULL, 100, 200);
```

SQL checks:

* NULL ❌
* NULL ❌
* 100 ✅

Output:

```text
100
```

---

# Example 2

Students Table

| name  | phone      |
| ----- | ---------- |
| Rahul | 9999999999 |
| Priya | NULL       |

Query:

```sql
SELECT
    name,
    COALESCE(phone, 'Not Available') AS phone
FROM Students;
```

Output:

| name  | phone         |
| ----- | ------------- |
| Rahul | 9999999999    |
| Priya | Not Available |

Instead of displaying `NULL`, SQL displays **"Not Available"**.

---

# Real-World Example

Suppose customers may not have an email address.

```sql
SELECT
    customer_name,
    COALESCE(email, 'No Email') AS email
FROM Customers;
```

This replaces missing emails with a readable message.

---

# ISNULL()

> **Note:** `ISNULL()` is mainly used in **SQL Server**. Other databases may use different functions.

## Syntax

```sql
ISNULL(expression, replacement)
```

Example:

```sql
SELECT ISNULL(phone, 'Not Available')
FROM Students;
```

Output:

| phone         |
| ------------- |
| 9999999999    |
| Not Available |

Think of it as:

> **If the value is NULL, replace it with another value.**

---

# COALESCE() vs ISNULL()

Both functions can replace NULL values.

Example:

```sql
COALESCE(phone, 'Not Available')
```

```sql
ISNULL(phone, 'Not Available')
```

Both return the same result in this case.

---

# Difference Between COALESCE() and ISNULL()

| COALESCE()                   | ISNULL()                           |
| ---------------------------- | ---------------------------------- |
| Accepts multiple values      | Accepts only one replacement value |
| SQL Standard                 | SQL Server specific                |
| Returns first non-NULL value | Replaces NULL with specified value |

Example using COALESCE:

```sql
SELECT COALESCE(NULL, NULL, NULL, 100);
```

Output:

```text
100
```

Example using ISNULL:

```sql
SELECT ISNULL(NULL, 100);
```

Output:

```text
100
```

---

# Why is COALESCE More Powerful?

Suppose we have:

| name  | mobile     | email                                     |
| ----- | ---------- | ----------------------------------------- |
| Rahul | NULL       | [rahul@gmail.com](mailto:rahul@gmail.com) |
| Priya | 9999999999 | NULL                                      |

Query:

```sql
SELECT
    name,
    COALESCE(mobile, email, 'No Contact') AS contact
FROM Users;
```

Output:

| name  | contact                                   |
| ----- | ----------------------------------------- |
| Rahul | [rahul@gmail.com](mailto:rahul@gmail.com) |
| Priya | 9999999999                                |

SQL returns the first available contact information.

---

# NULL Handling in Calculations

Employees Table

| name  | bonus |
| ----- | ----- |
| Rahul | 5000  |
| Priya | NULL  |

Query:

```sql
SELECT bonus + 1000
FROM Employees;
```

Output:

| Result |
| ------ |
| 6000   |
| NULL   |

Because:

```text
NULL + 1000 = NULL
```

To fix this:

```sql
SELECT COALESCE(bonus, 0) + 1000 AS TotalBonus
FROM Employees;
```

Output:

| TotalBonus |
| ---------- |
| 6000       |
| 1000       |

Now, missing bonuses are treated as `0`.

---

# Checking for NULL Values

A common mistake is writing:

❌ Wrong:

```sql
WHERE phone = NULL;
```

This **never returns any rows**.

The correct way is:

```sql
WHERE phone IS NULL;
```

This returns all rows where the phone number is missing.

Example:

```sql
SELECT *
FROM Students
WHERE phone IS NULL;
```

---

# Finding Non-NULL Values

To find rows where a value exists:

```sql
WHERE phone IS NOT NULL;
```

Example:

```sql
SELECT *
FROM Students
WHERE phone IS NOT NULL;
```

This returns only students with phone numbers.

---

# Common Use Cases

* Replacing missing values
* Handling calculations involving NULL
* Finding incomplete records
* Displaying user-friendly messages
* Choosing the first available value from multiple columns

---

# Quick Reference

```sql
-- Replace NULL values
SELECT COALESCE(phone, 'Not Available')
FROM Students;

-- SQL Server only
SELECT ISNULL(phone, 'Not Available')
FROM Students;

-- Find NULL values
SELECT *
FROM Students
WHERE phone IS NULL;

-- Find non-NULL values
SELECT *
FROM Students
WHERE phone IS NOT NULL;

-- Handle calculations
SELECT COALESCE(bonus, 0) + 1000
FROM Employees;
```

---

# Memory Tricks

### COALESCE

> **"Give me the first value that exists."**

Checks multiple values and returns the first non-NULL one.

---

### ISNULL

> **"If this value is NULL, replace it."**

Checks only one value and one replacement.

---

### IS NULL

Used to find missing values.

```sql
WHERE column IS NULL;
```

---

### IS NOT NULL

Used to find available values.

```sql
WHERE column IS NOT NULL;
```

---

# Common Interview Questions

## What is NULL?

A missing or unknown value in SQL.

---

## What is the difference between COALESCE() and ISNULL()?

**COALESCE()**

* SQL Standard
* Accepts multiple values
* Returns the first non-NULL value

**ISNULL()**

* SQL Server specific
* Accepts one value and one replacement
* Replaces NULL values

---

## Why can't we use `= NULL`?

Because `NULL` represents an unknown value.

Always use:

```sql
IS NULL
```

or

```sql
IS NOT NULL
```

---

# Small Note for DA Learning

As a Data Analyst, you'll frequently encounter missing data. Knowing how to handle `NULL` values correctly is essential for accurate reporting and analysis.

You'll often use:

* `COALESCE()` to replace missing values
* `IS NULL` to find incomplete records
* `IS NOT NULL` to filter valid data

NULL handling is one of the most commonly tested SQL concepts in placements, coding assessments, and Data Analyst interviews.
