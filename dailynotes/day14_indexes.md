Day 14 --> Indexes
Indexes are used to speed up data retrieval from a table. If your query is correct but slow, indexes are often the first thing to check.

What is an Index?
An index is a special lookup structure created on one or more columns of a table to help the database find rows faster.

Think of it like the index page of a book: instead of reading every page to find a topic, you jump directly to the page number you need.

Important: An index improves read/query speed, but it can make INSERT, UPDATE, DELETE slightly slower because the index also needs to be updated.

Why Do We Use Indexes?
Without an index, the database may scan the entire table to find matching rows.

With an index, the database can quickly locate the required rows.

Indexes are useful when:

a column is frequently used in WHERE
a column is frequently used in JOIN
a column is frequently used in ORDER BY
a column is frequently used in GROUP BY
Basic Syntax
sql


CREATE INDEX index_name
ON table_name (column_name);
Example:

sql


CREATE INDEX idx_emp_name
ON employees (emp_name);
This creates an index on the emp_name column.

Example Without Understanding Performance Tooling
Suppose you have a large employees table and often run:

sql


SELECT * FROM employees
WHERE emp_name = 'Aman';
If emp_name has no index, the database may check row by row.

If emp_name has an index, the search becomes much faster.

The bigger the table, the more useful an index usually becomes.

Index on Multiple Columns
You can also create an index on more than one column.

sql


CREATE INDEX idx_region_salary
ON employees (region, salary);
This is called a composite index.

It is useful when queries often use both columns together, like:

sql


SELECT * FROM employees
WHERE region = 'North' AND salary > 50000;
Order matters in composite indexes. An index on (region, salary) is most useful when the query starts filtering with region.

Unique Index
A unique index prevents duplicate values in a column.

sql


CREATE UNIQUE INDEX idx_email
ON employees (email);
This ensures every email is different.

In many databases, PRIMARY KEY and UNIQUE constraints automatically create indexes behind the scenes.

Drop an Index
If you no longer need an index, you can remove it.

sql


DROP INDEX idx_emp_name;
Syntax for dropping an index can vary slightly by database. In some systems, you may need to mention the table name too.

Important Trade-Off
Indexes are helpful, but too many indexes are not good.

Why?

They take extra storage
They slow down INSERT, UPDATE, and DELETE
Unused indexes add maintenance cost without benefit
So, create indexes on columns that are queried often, not on every column.

Common Use Cases
Searching employees by emp_id
Filtering orders by order_date
Joining customers.customer_id with orders.customer_id
Sorting sales by revenue
Grouping records by region
When an Index Helps Less
Indexes may not help much when:

the table is very small
the column has very few unique values
you are selecting almost every row
functions are applied directly on the indexed column
Example:

sql


SELECT * FROM employees
WHERE UPPER(emp_name) = 'AMAN';
This may reduce index usage in many databases.

Better approach in some cases: store clean data or use database-specific indexing strategies.

Primary Key and Index
A PRIMARY KEY is usually indexed automatically.

Example:

sql


CREATE TABLE employees (
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(50),
    region VARCHAR(20)
);
Here, emp_id usually gets an index automatically.

Quick Example
sql


CREATE TABLE sales_data (
    sale_id INT PRIMARY KEY,
    customer_id INT,
    region VARCHAR(20),
    revenue INT
);
If you often run:

sql


SELECT * FROM sales_data
WHERE customer_id = 101;
Then creating this index is useful:

sql


CREATE INDEX idx_customer_id
ON sales_data (customer_id);
When to Use an Index
Use an index when a column is frequently used for searching, joining, sorting, or grouping - especially on large tables.

Do not create indexes blindly. Always think: "Will this column be searched often enough to justify it?"

Index vs Full Table Scan
Index	Full Table Scan
Speed	Faster for targeted lookups	Slower on large tables
Storage	Needs extra space	No extra space
Best for	Frequent filters and joins	Small tables or broad reads
Write operations	Slightly slower	No index maintenance
🧠 Memory Tricks
Index = "shortcut to find rows faster"

Used on:

WHERE
JOIN
ORDER BY
GROUP BY
Trade-off:

faster reading
slower writing
Composite index: (col1, col2) -> order matters

⚡ Quick Reference
sql


-- Create index
CREATE INDEX idx_name
ON table_name (column_name);
-- Create composite index
CREATE INDEX idx_multi
ON table_name (col1, col2);
-- Create unique index
CREATE UNIQUE INDEX idx_unique
ON table_name (column_name);
-- Basic query that benefits from index
SELECT * FROM table_name
WHERE column_name = 'value';
-- Drop index
DROP INDEX idx_name;

