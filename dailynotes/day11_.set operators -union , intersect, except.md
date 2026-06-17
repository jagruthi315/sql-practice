# Day 11 --> Set Operators — UNION, INTERSECT, EXCEPT


Week 3 begins! Today is about Set Operators —
another way to combine tables, but this time
we're stacking **rows** not adding columns.

---

## Quick Recap — SET Operators vs JOINs

| | SET Operators | JOINs |
|--|--------------|-------|
| Combines | Rows (vertically) | Columns (horizontally) |
| Needs | Same number of columns + same data types | A key column |
| Examples | UNION, INTERSECT, EXCEPT | INNER, LEFT, RIGHT, FULL |

---

## The Golden Rule for SET Operators

> Both tables MUST have:
> - Same **number of columns**
> - Same **data types** in each column
> - Order of columns must match

```sql
-- ✅ Valid — both have 2 columns of same types
SELECT id, name FROM table_a
UNION
SELECT id, name FROM table_b;

-- ❌ Invalid — different number of columns
SELECT id, name, city FROM table_a
UNION
SELECT id, name FROM table_b;
```

---

## UNION — Combine + Remove Duplicates

Combines results of two queries and removes duplicate rows.

```sql
SELECT name FROM customers_2023
UNION
SELECT name FROM customers_2024;
```

Example:
customers_2023    customers_2024

Aman              Aman

Priya             Riya

Karan             Karan
UNION result:

Aman   ← duplicate removed

Priya

Karan  ← duplicate removed

Riya

> UNION = combine everything, show each value only ONCE

---

## UNION ALL — Combine + Keep Duplicates

Same as UNION but keeps ALL rows including duplicates.
Also faster than UNION because it skips the duplicate check.

```sql
SELECT name FROM customers_2023
UNION ALL
SELECT name FROM customers_2024;
```
UNION ALL result:

Aman   ← appears twice (kept both)

Priya

Karan  ← appears twice (kept both)

Aman

Riya

Karan

> Use UNION ALL when you know there are no duplicates
> or when you actually want to keep them — it's faster.

---

## INTERSECT — Only Common Rows

Returns only rows that appear in BOTH queries.
Like INNER JOIN but for rows.

```sql
SELECT name FROM customers_2023
INTERSECT
SELECT name FROM customers_2024;
```
customers_2023    customers_2024

Aman              Aman      ✅ common

Priya             Riya

Karan             Karan     ✅ common
INTERSECT result:

Aman

Karan

> INTERSECT = "what's in both lists?"

---

## EXCEPT — Rows in First but NOT in Second

Returns rows from the first query that don't appear
in the second query. Also called MINUS in Oracle SQL.

```sql
SELECT name FROM customers_2023
EXCEPT
SELECT name FROM customers_2024;
```
customers_2023    customers_2024

Aman              Aman      ❌ exists in both, removed

Priya             Riya

Karan             Karan     ❌ exists in both, removed
EXCEPT result:

Priya   ← only in 2023, not in 2024

> EXCEPT = "what's in A but NOT in B?"

---

## All Four Together — Visual Summary
Table A: Aman, Priya, Karan

Table B: Aman, Riya, Karan
UNION      → Aman, Priya, Karan, Riya     (all, no duplicates)

UNION ALL  → Aman, Priya, Karan, Aman, Riya, Karan  (all, with duplicates)

INTERSECT  → Aman, Karan                  (only common)

EXCEPT     → Priya                         (in A but not B)

---

## Real Life Examples

```sql
-- All employees from Delhi OR Mumbai (no duplicates)
SELECT name FROM employees WHERE city = 'Delhi'
UNION
SELECT name FROM employees WHERE city = 'Mumbai';

-- Customers who ordered in BOTH 2023 AND 2024
SELECT customer_id FROM orders_2023
INTERSECT
SELECT customer_id FROM orders_2024;

-- Customers who ordered in 2023 but NOT in 2024
-- (lapsed customers — useful for marketing!)
SELECT customer_id FROM orders_2023
EXCEPT
SELECT customer_id FROM orders_2024;
```

---

## UNION vs UNION ALL — When to Use Which?

| | UNION | UNION ALL |
|--|-------|-----------|
| Removes duplicates | ✅ Yes | ❌ No |
| Speed | 🐢 Slower | ⚡ Faster |
| Use when | duplicates possible | no duplicates / want all rows |

---

## 🧠 Memory Tricks
UNION      → "combine, clean" (no duplicates)

UNION ALL  → "combine, keep all" (with duplicates)

INTERSECT  → "what's common?" (both lists)

EXCEPT     → "what's only in A?" (A minus B)
SET Operators = stacking rows vertically

JOINs = adding columns horizontally

---

## ⚡ Quick Reference

```sql
-- UNION (no duplicates)
SELECT col FROM table_a
UNION
SELECT col FROM table_b;

-- UNION ALL (keep duplicates)
SELECT col FROM table_a
UNION ALL
SELECT col FROM table_b;

-- INTERSECT (common rows only)
SELECT col FROM table_a
INTERSECT
SELECT col FROM table_b;

-- EXCEPT (in A but not B)
SELECT col FROM table_a
EXCEPT
SELECT col FROM table_b;
```
