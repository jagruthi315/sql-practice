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
