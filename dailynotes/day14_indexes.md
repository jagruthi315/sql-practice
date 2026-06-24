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
What is a View?

A View is a saved SQL query that behaves like a table.

Think of it as a shortcut to a query that you use frequently.

Instead of writing the same long query again and again, you can save it as a view and query the view directly.

Why Do We Use Views?

Views are commonly used to:

Simplify complex queries
Reuse frequently used SQL logic
Hide unnecessary columns
Restrict access to sensitive data
Improve readability of reports and dashboards
Basic Syntax
CREATE VIEW view_name AS
SELECT column1, column2
FROM table_name;

Example:

CREATE VIEW employee_details AS
SELECT emp_id, emp_name, department
FROM employees;

Now you can query the view just like a table:

SELECT *
FROM employee_details;
Example Without a View

Suppose you frequently run:

SELECT emp_id,
       emp_name,
       department
FROM employees
WHERE department = 'Sales';

Instead of writing this query repeatedly, create a view:

CREATE VIEW sales_employees AS
SELECT emp_id,
       emp_name,
       department
FROM employees
WHERE department = 'Sales';

Now simply run:

SELECT *
FROM sales_employees;
View Using Multiple Tables

Views become especially useful when joins are involved.

Example:

CREATE VIEW employee_orders AS
SELECT e.emp_id,
       e.emp_name,
       o.order_id,
       o.order_amount
FROM employees e
JOIN orders o
ON e.emp_id = o.emp_id;

Now analysts can access joined information without repeatedly writing the JOIN.

SELECT *
FROM employee_orders;
Updating Data Through a View

In some databases, simple views can be updated.

Example:

UPDATE employee_details
SET department = 'HR'
WHERE emp_id = 101;

Whether this works depends on the database and the complexity of the view.

Views containing joins, aggregates, GROUP BY, DISTINCT, etc., are often not directly updatable.

View with Aggregate Functions

Views can also store summarized data.

Example:

CREATE VIEW department_salary_summary AS
SELECT department,
       AVG(salary) AS avg_salary
FROM employees
GROUP BY department;

Querying the view:

SELECT *
FROM department_salary_summary;

This is useful for dashboards and reporting.

Replace or Modify a View

Some databases support:

CREATE OR REPLACE VIEW employee_details AS
SELECT emp_id,
       emp_name,
       department,
       salary
FROM employees;

This updates the existing view definition.

Note: Support varies by database.

Drop a View

If a view is no longer needed:

DROP VIEW employee_details;

The underlying table remains unchanged.

Only the view is removed.

Important Characteristics of Views

A view:

✅ Stores a query

✅ Behaves like a table

✅ Can simplify complex SQL

✅ Helps with security

❌ Usually does not store actual data

❌ Is not necessarily faster than the original query

Views vs Tables
Feature	View	Table
Stores Data	No (usually)	Yes
Based On Query	Yes	No
Physical Storage	Minimal	Uses storage
Can Join Tables	Yes	N/A
Useful For Reporting	Very	Moderate
Views for Security

Suppose the employees table contains salary information:

SELECT *
FROM employees;
emp_id	emp_name	department	salary
101	Aman	Sales	70000

You may not want everyone to see salary data.

Create a view:

CREATE VIEW employee_public AS
SELECT emp_id,
       emp_name,
       department
FROM employees;

Now users can query:

SELECT *
FROM employee_public;

without seeing salary information.

Common Use Cases
Dashboard reporting
Data analyst reporting layers
Hiding sensitive columns
Simplifying joins
Creating reusable business logic
Building BI tool datasets
Sharing cleaned data with teams
View vs CTE
Feature	View	CTE
Saved Permanently	Yes	No
Reusable	Yes	Only within query
Requires Creation	Yes	No
Good For Reports	Yes	Usually No
Scope	Database-wide	Current query only

Example CTE:

WITH sales_data AS (
    SELECT *
    FROM employees
    WHERE department = 'Sales'
)
SELECT *
FROM sales_data;

After execution, the CTE disappears.

A View remains in the database until dropped.

View vs Index
Feature	View	Index
Purpose	Simplify queries	Speed up queries
Stores Query Logic	Yes	No
Improves Readability	Yes	No
Improves Performance	Usually No	Yes
Acts Like Table	Yes	No
Quick Example

Create table:

CREATE TABLE sales (
    sale_id INT,
    customer_id INT,
    revenue INT
);

Create view:

CREATE VIEW high_value_sales AS
SELECT *
FROM sales
WHERE revenue > 50000;

Query view:

SELECT *
FROM high_value_sales;
When to Use a View

Use a view when:

You repeatedly write the same query
Queries contain multiple joins
You want cleaner SQL
You need to hide sensitive data
You are creating reports or dashboards
Memory Tricks

View = "Saved SQL Query"

Think:

View → Simplicity

Index → Speed

Table → Actual Data

A view behaves like a table but usually does not store data itself.

Quick Reference
-- Create View
CREATE VIEW view_name AS
SELECT *
FROM table_name;

-- Query View
SELECT *
FROM view_name;

-- Create View with Join
CREATE VIEW employee_orders AS
SELECT e.emp_name,
       o.order_id
FROM employees e
JOIN orders o
ON e.emp_id = o.emp_id;

-- Replace View (supported in many DBs)
CREATE OR REPLACE VIEW view_name AS
SELECT * FROM table_name;

-- Drop View
DROP VIEW view_name;
Small Note for DA Learning

For a Data Analyst, Views are extremely useful because they allow you to:

Save frequently used business queries
Build cleaner reporting datasets
Avoid rewriting complex joins
Share analysis-ready data with BI tools like Power BI and Tableau

In real-world analytics teams, you'll often work with views every day, even more frequently than creating indexes yourself.
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


