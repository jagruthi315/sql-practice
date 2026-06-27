# Day 18 --> String & Date Functions

String and Date functions are among the most commonly used SQL functions in interviews, coding platforms like HackerRank, and real-world data analysis.

They help us clean text, manipulate strings, and work with dates efficiently.

---

# String Functions

String functions work on text values.

Suppose we have the following table:

| id | name  |
| -- | ----- |
| 1  | Rahul |
| 2  | Priya |
| 3  | rohan |

---

# 1. LENGTH()

Returns the number of characters in a string.

### Syntax

```sql
LENGTH(string)
```

Example:

```sql
SELECT LENGTH('Rahul');
```

Output:

```
5
```

Using a table:

```sql
SELECT
    name,
    LENGTH(name) AS NameLength
FROM Students;
```

---

# 2. UPPER()

Converts text into uppercase.

### Syntax

```sql
UPPER(string)
```

Example:

```sql
SELECT UPPER('rahul');
```

Output:

```
RAHUL
```

---

# 3. LOWER()

Converts text into lowercase.

### Syntax

```sql
LOWER(string)
```

Example:

```sql
SELECT LOWER('RAHUL');
```

Output:

```
rahul
```

---

# 4. CONCAT()

Joins two or more strings together.

### Syntax

```sql
CONCAT(string1, string2, ...)
```

Example:

```sql
SELECT CONCAT('Rahul', ' ', 'Sharma');
```

Output:

```
Rahul Sharma
```

Using columns:

```sql
SELECT CONCAT(first_name, ' ', last_name)
FROM Employees;
```

---

# 5. SUBSTRING()

Extracts a portion of a string.

### Syntax

```sql
SUBSTRING(string, start_position, length)
```

Example:

```sql
SELECT SUBSTRING('Rahul', 1, 3);
```

Output:

```
Rah
```

Explanation:

* Original String → Rahul
* Start Position → 1
* Number of Characters → 3

Result:

```
Rah
```

---

# 6. TRIM()

Removes extra spaces from the beginning and end of a string.

### Syntax

```sql
TRIM(string)
```

Example:

```sql
SELECT TRIM('   Rahul   ');
```

Output:

```
Rahul
```

Useful when cleaning messy datasets.

---

# 7. REPLACE()

Replaces one piece of text with another.

### Syntax

```sql
REPLACE(original_string, old_text, new_text)
```

Example:

```sql
SELECT REPLACE('I love SQL', 'SQL', 'Python');
```

Output:

```
I love Python
```

### Understanding the Parameters

| Parameter | Value          | Meaning          |
| --------- | -------------- | ---------------- |
| 1st       | `'I love SQL'` | Original String  |
| 2nd       | `'SQL'`        | Text to Find     |
| 3rd       | `'Python'`     | Replacement Text |

Think of it as:

> In the string **"I love SQL"**, find **"SQL"** and replace it with **"Python"**.

---

### More Examples

Example 1

```sql
SELECT REPLACE('banana', 'a', 'x');
```

Output:

```
bxnxnx
```

Notice that **all occurrences** are replaced.

---

Example 2

```sql
SELECT REPLACE('hello world', 'world', 'SQL');
```

Output:

```
hello SQL
```

---

Example 3

Using a table:

| name         |
| ------------ |
| Rahul Sharma |
| Priya Sharma |

Query:

```sql
SELECT REPLACE(name, 'Sharma', 'Singh')
FROM Students;
```

Output:

| Result      |
| ----------- |
| Rahul Singh |
| Priya Singh |

---

### Interview Trick Question

```sql
SELECT REPLACE('I love SQL', 'Python', 'Java');
```

Output:

```
I love SQL
```

Why?

Because `"Python"` does not exist in the original string, so nothing is replaced.

---

### Memory Trick

Think of REPLACE as:

```text
REPLACE(
    WHERE_TO_LOOK,
    WHAT_TO_FIND,
    WHAT_TO_PUT
)
```

or

```text
REPLACE(
    Original String,
    Old Value,
    New Value
)
```

---

# 8. LEFT()

Returns characters from the left side of a string.

### Syntax

```sql
LEFT(string, number_of_characters)
```

Example:

```sql
SELECT LEFT('Rahul', 3);
```

Output:

```
Rah
```

---

# 9. RIGHT()

Returns characters from the right side of a string.

### Syntax

```sql
RIGHT(string, number_of_characters)
```

Example:

```sql
SELECT RIGHT('Rahul', 2);
```

Output:

```
ul
```

---

# 10. POSITION() / INSTR()

Returns the position of a character inside a string.

Example:

```sql
SELECT POSITION('a' IN 'Rahul');
```

Output:

```
2
```

Some databases use `INSTR()` instead of `POSITION()`.

---

# Common HackerRank Questions Using String Functions

These functions are frequently used in problems like:

* Weather Observation Station
* The PADS
* Employee Names
* Higher Than 75 Marks

---

# Date Functions

Date functions help us work with dates and time.

Suppose we have:

| id | order_date |
| -- | ---------- |
| 1  | 2025-06-17 |
| 2  | 2025-06-18 |

---

# 1. CURRENT_DATE

Returns today's date.

```sql
SELECT CURRENT_DATE;
```

Output:

```
2025-06-17
```

---

# 2. NOW()

Returns the current date and time.

```sql
SELECT NOW();
```

Output:

```
2025-06-17 14:30:45
```

---

# 3. YEAR()

Extracts the year from a date.

```sql
SELECT YEAR('2025-06-17');
```

Output:

```
2025
```

---

# 4. MONTH()

Extracts the month.

```sql
SELECT MONTH('2025-06-17');
```

Output:

```
6
```

---

# 5. DAY()

Extracts the day.

```sql
SELECT DAY('2025-06-17');
```

Output:

```
17
```

Using a table:

```sql
SELECT YEAR(order_date)
FROM Orders;
```

---

# 6. DATEDIFF()

Returns the difference between two dates.

```sql
SELECT DATEDIFF('2025-06-20', '2025-06-17');
```

Output:

```
3
```

Meaning:

```
20 - 17 = 3 Days
```

---

# 7. DATE_ADD()

Adds a specified number of days to a date.

```sql
SELECT DATE_ADD(
    '2025-06-17',
    INTERVAL 10 DAY
);
```

Output:

```
2025-06-27
```

---

# 8. DATE_SUB()

Subtracts days from a date.

```sql
SELECT DATE_SUB(
    '2025-06-17',
    INTERVAL 5 DAY
);
```

Output:

```
2025-06-12
```

---

# 9. EXTRACT()

Extracts a specific part of a date.

```sql
SELECT EXTRACT(YEAR FROM '2025-06-17');
```

Output:

```
2025
```

---

# Real Interview Examples

Find all orders placed in 2025.

```sql
SELECT *
FROM Orders
WHERE YEAR(order_date) = 2025;
```

---

Find employees whose names start with A.

```sql
SELECT *
FROM Employees
WHERE name LIKE 'A%';
```

---

Find orders placed this month.

```sql
SELECT *
FROM Orders
WHERE MONTH(order_date) = MONTH(CURRENT_DATE);
```

---

# Quick Reference

## String Functions

| Function             | Purpose                 |
| -------------------- | ----------------------- |
| LENGTH()             | Count characters        |
| UPPER()              | Convert to uppercase    |
| LOWER()              | Convert to lowercase    |
| CONCAT()             | Join strings            |
| SUBSTRING()          | Extract text            |
| TRIM()               | Remove spaces           |
| REPLACE()            | Replace text            |
| LEFT()               | Left characters         |
| RIGHT()              | Right characters        |
| POSITION() / INSTR() | Find character position |

---

## Date Functions

| Function     | Purpose                  |
| ------------ | ------------------------ |
| CURRENT_DATE | Today's date             |
| NOW()        | Current date and time    |
| YEAR()       | Extract year             |
| MONTH()      | Extract month            |
| DAY()        | Extract day              |
| DATEDIFF()   | Difference between dates |
| DATE_ADD()   | Add days                 |
| DATE_SUB()   | Subtract days            |
| EXTRACT()    | Extract date parts       |

---

# Functions to Memorize First

## String Functions

1. LENGTH()
2. CONCAT()
3. SUBSTRING()
4. UPPER()
5. LOWER()
6. REPLACE()

---

## Date Functions

1. YEAR()
2. MONTH()
3. DAY()
4. DATEDIFF()
5. CURRENT_DATE
6. NOW()

These functions cover around **80% of beginner and intermediate SQL function questions** asked in coding assessments and interviews.

---

# Common Interview Question

Whenever you learn a SQL function, ask yourself these three questions:

1. **What does this function do?**
2. **What are its parameters (inputs)?**
3. **What does it return (output)?**

For example:

```sql
REPLACE(
    original_string,
    old_text,
    new_text
)
```

* **Input 1:** Original string
* **Input 2:** Text to find
* **Input 3:** Replacement text
* **Output:** A new string with the replacement applied

This habit makes it much easier to understand and remember SQL functions.

---

# Small Note for DA Learning

As a Data Analyst, you'll use string and date functions almost every day for cleaning, transforming, and analyzing data. These functions are essential for writing efficient SQL queries and are among the most frequently tested topics in SQL interviews, HackerRank challenges, and real-world analytics projects.
