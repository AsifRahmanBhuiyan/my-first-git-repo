1. What is PostgreSQL?
This question checks your basic understanding of a relational database system and why PostgreSQL is often chosen over others. It lays the foundation for all further database-related topics.

PostgreSQL is an open-source, object-relational database management system (ORDBMS) that supports both traditional relational data and more complex data types (like JSON, XML, arrays).

It follows the SQL standard but also offers advanced capabilities such as:
- Full-text search
- Window functions
- Triggers
- Custom functions in languages like SQL, PL/pgSQL, Python, etc.
- Geographic data via PostGIS


Real-world usage example:
Let’s say you’re building an online bookstore. You’d use PostgreSQL to:
- Store books (title, author, price)
- Track customers and their orders
- Search across titles using full-text search
- Enforce data consistency (e.g., order must have a valid customer)



2. What is the purpose of a database schema in PostgreSQL?
This checks whether you understand how to organize database objects logically. It’s about managing structure and accessibility within a large database.
A schema is like a namespace or a folder within a PostgreSQL database. It contains tables, views, functions, and other database objects. Schemas help in:
- Organizing related tables (e.g., grouping all HR tables in one schema)
- Avoiding naming conflicts (you can have two tables named users in different schemas)
- Managing user permissions (restrict access to sensitive schemas)


Example:
CREATE SCHEMA hr;
CREATE TABLE hr.employees (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    department_id INT
);
Now if you also have a marketing.employees table, PostgreSQL keeps them separate. You can even grant HR staff access to only the hr schema.


3. Explain the Primary Key and Foreign Key concepts in PostgreSQL.
This tests your understanding of data integrity and relationships between tables, which are core to relational database design.
- A Primary Key (PK) uniquely identifies each row in a table. It must be unique and not null.
- A Foreign Key (FK) enforces a relationship between two tables. It links a column in one table to the Primary Key of another, ensuring data consistency.


Example:
CREATE TABLE departments (
    department_id SERIAL PRIMARY KEY,
    name VARCHAR(50)
);

CREATE TABLE employees (
    employee_id SERIAL PRIMARY KEY,
    name VARCHAR(50),
    department_id INT REFERENCES departments(department_id)
);

Now you can only add employees to valid departments. If you try to insert an employee with a department_id that doesn't exist, PostgreSQL will raise an error.
This enforces referential integrity, preventing orphaned or invalid relationships.

4. What is the difference between the VARCHAR and CHAR data types?
This is about understanding how text is stored and managed in the database, and the trade-offs between efficiency and performance.
Feature

Feature: Storage
VARCHAR(n): Stores only the characters used.
CHAR(n): Pads with spaces to fill the fixed length n.

Feature: Efficiency
VARCHAR(n): More space-efficient for variable-length text.
CHAR(n): Less efficient when storing varying-length data.

Feature: Use Case
VARCHAR(n): Suitable for names, addresses, descriptions.
CHAR(n): Suitable for fixed-length codes like country codes or status flags.

Feature: Performance
VARCHAR(n): May have slight overhead due to dynamic sizing.
CHAR(n): Slightly faster when dealing with fixed-length values.

Example:
name VARCHAR(50)    -- good for names of varying length
status CHAR(1)      -- good for single-letter codes like 'A' (Active), 'I' (Inactive)

If you define CHAR(10) and insert 'Hi', it stores it as 'Hi ' with 8 trailing spaces.
Best practice: Use VARCHAR in most cases. Use CHAR only for fixed-length data where performance matters slightly.


5. Explain the purpose of the WHERE clause in a SELECT statement.
The WHERE clause is fundamental for querying only the data you need, rather than retrieving everything. This is about data filtering and retrieval efficiency.
The WHERE clause is used to filter rows in a query based on a condition. Without WHERE, a query would return all rows, which can be inefficient and overwhelming.
Example 1: Basic filtering
SELECT * FROM employees
WHERE department_id = 2;

Returns only employees in department 2.
Example 2: Multiple conditions
SELECT * FROM products
WHERE price > 100 AND in_stock = true;

Filters products to show only those that are in stock and cost more than 100.
You can use various operators:
=, !=, <, >, BETWEEN, LIKE, IN, IS NULL, etc.


Why it's important:
- In real applications, you rarely want to retrieve all data.
- Helps with performance, security, and user-specific views of data.


