# Day 6 --> GROUP BY, HAVING, DISTINCT

Week 2 starts now — this is where SQL gets actually interesting.
Till now we were just fetching data. Today we learn how to
**summarize and group** it — which is what real data analysis looks like.

---

## DISTINCT — Remove Duplicates

The simplest one. If your table has repeated values and you only
want to see unique ones, use DISTINCT.

```sql
-- Without DISTINCT — shows duplicates
SELECT employee_city FROM employees;
-- Delhi, Delhi, Mumbai, Noida, Delhi...

-- With DISTINCT — only unique values
SELECT DISTINCT employee_city FROM employees;
-- Delhi, Mumbai, Noida...
```

### Other uses of DISTINCT

```sql
-- With multiple columns
SELECT DISTINCT city, salary FROM employees;

-- Inside COUNT — count only unique cities
SELECT COUNT(DISTINCT employee_city) FROM employees;
```

> Think of DISTINCT like "show me each value only once"

---

## GROUP BY — Group Rows Together

GROUP BY groups rows that have the same value in a column
and lets you summarize each group.

Think of it like a pivot table in Excel — group by one column,
summarize with another.

**Real life example:**
"How many employees are there in each city?"
Instead of counting manually, SQL groups them for you.

```sql
SELECT employee_city, COUNT(employee_id)
FROM employees
GROUP BY employee_city;
```

Output:
| employee_city | count(employee_id) |
|--------------|-------------------|
| Delhi | 5 |
| Mumbai | 3 |
| Noida | 2 |

### How GROUP BY works internally
FROM employees          → get all rows
GROUP BY employee_city  → put same cities together
COUNT(employee_id)      → count each group
SELECT                  → show the result

> GROUP BY always goes **after** WHERE and **before** HAVING

---

## HAVING — Filter After Grouping

Once you have your groups, HAVING lets you filter them.

**Real life example:**
"Show me only cities where more than 2 employees work."

```sql
SELECT employee_city, COUNT(employee_id)
FROM employees
GROUP BY employee_city
HAVING COUNT(employee_id) > 2;
```

Output:
| employee_city | count(employee_id) |
|--------------|-------------------|
| Delhi | 5 |

Only Delhi had more than 2 employees, so only Delhi shows up.

### HAVING with SUM — from your notes example

```sql
SELECT Country, SUM(score)
FROM table
GROUP BY Country
HAVING SUM(score) > 800;
```

Step by step what happens:
1. FROM — get all rows from table
2. WHERE — filter rows before grouping (if any)
3. GROUP BY Country — group rows by country
4. SUM(score) — add up scores per group
5. HAVING — keep only groups where sum > 800

From the example table:
| Country | SUM(score) | Passes? |
|---------|-----------|---------|
| Germany | 850 | ✅ |
| USA | 900 | ✅ |
| UK | 750 | ❌ |

---
