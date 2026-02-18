Here are **short and crisp answers** to all 30 SQL interview questions, with queries where needed:

---

# 🔹 Basic SQL Questions

### 1. What is SQL?

SQL (Structured Query Language) is used to manage and manipulate relational databases.

---

### 2. Types of SQL commands?

* **DDL** – Data Definition (CREATE, DROP, ALTER)
* **DML** – Data Manipulation (INSERT, UPDATE, DELETE)
* **DCL** – Data Control (GRANT, REVOKE)
* **TCL** – Transaction Control (COMMIT, ROLLBACK)

---

### 3. Common SQL Data Types

* INT
* VARCHAR
* DATE
* FLOAT
* BOOLEAN
* CHAR

---

### 4. What is a Primary Key?

A column that uniquely identifies each row.

* No duplicates
* No NULL values

---

### 5. What is a Foreign Key?

A column that links to a primary key in another table to maintain referential integrity.

---

### 6. PRIMARY KEY vs UNIQUE

| PRIMARY KEY        | UNIQUE                        |
| ------------------ | ----------------------------- |
| No NULLs allowed   | Allows one NULL (in most DBs) |
| Only one per table | Multiple allowed              |

---

### 7. DELETE vs TRUNCATE vs DROP

| DELETE        | TRUNCATE         | DROP              |
| ------------- | ---------------- | ----------------- |
| Removes rows  | Removes all rows | Deletes table     |
| Can use WHERE | No WHERE         | Removes structure |
| Can rollback  | Usually cannot   | Cannot rollback   |

---

### 8. What is WHERE?

Filters rows based on a condition.

```sql
SELECT * FROM employees WHERE salary > 50000;
```

---

### 9. WHERE vs HAVING

* **WHERE** filters rows before GROUP BY
* **HAVING** filters groups after GROUP BY

```sql
SELECT dept_id, COUNT(*) 
FROM employees 
GROUP BY dept_id
HAVING COUNT(*) > 5;
```

---

### 10. What is GROUP BY?

Groups rows with same values.

```sql
SELECT dept_id, COUNT(*) 
FROM employees 
GROUP BY dept_id;
```

---

# 🔹 Intermediate SQL Questions

### 11. What is a JOIN?

Used to combine data from multiple tables.

Types:

* INNER JOIN
* LEFT JOIN
* RIGHT JOIN
* FULL JOIN

---

### 12. INNER JOIN vs LEFT JOIN

* **INNER JOIN** → returns matching rows only
* **LEFT JOIN** → returns all rows from left table + matched rows

```sql
SELECT e.name, d.dept_name
FROM employees e
LEFT JOIN departments d
ON e.dept_id = d.id;
```

---

### 13. What is a Subquery?

Query inside another query.

```sql
SELECT * 
FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```

---

### 14. What is a Correlated Subquery?

Subquery that depends on outer query.

```sql
SELECT e1.name
FROM employees e1
WHERE salary > (
  SELECT AVG(salary)
  FROM employees e2
  WHERE e2.dept_id = e1.dept_id
);
```

---

### 15. IN vs EXISTS

* **IN** compares values
* **EXISTS** checks for existence of rows
* EXISTS is faster for large datasets

---

### 16. What is Normalization?

Process of organizing data to reduce redundancy.

---

### 17. Types of Normalization

* 1NF – No repeating groups
* 2NF – No partial dependency
* 3NF – No transitive dependency
* BCNF – Stronger version of 3NF

---

### 18. What is Denormalization?

Adding redundancy to improve performance.

---

### 19. What is an Index?

Improves search performance on columns.

---

### 20. Clustered vs Non-clustered Index

| Clustered         | Non-clustered      |
| ----------------- | ------------------ |
| Sorts actual data | Separate structure |
| One per table     | Multiple allowed   |

---

# 🔹 Query-Based Questions

---

### 21. Second Highest Salary

```sql
SELECT MAX(salary)
FROM employees
WHERE salary < (SELECT MAX(salary) FROM employees);
```

---

### 22. Remove Duplicate Records

```sql
DELETE FROM employees
WHERE id NOT IN (
  SELECT MIN(id)
  FROM employees
  GROUP BY name, salary
);
```

---

### 23. Names starting with 'A'

```sql
SELECT * FROM employees
WHERE name LIKE 'A%';
```

---

### 24. Count employees in each department

```sql
SELECT dept_id, COUNT(*)
FROM employees
GROUP BY dept_id;
```

---

### 25. Fetch duplicate records

```sql
SELECT name, COUNT(*)
FROM employees
GROUP BY name
HAVING COUNT(*) > 1;
```

---

### 26. Nth Highest Salary

```sql
SELECT salary
FROM employees
ORDER BY salary DESC
LIMIT 1 OFFSET n-1;
```

(Replace n with required rank)

---

### 27. Records between two dates

```sql
SELECT *
FROM employees
WHERE joining_date BETWEEN '2024-01-01' AND '2024-12-31';
```

---

### 28. Common records from two tables

```sql
SELECT id FROM table1
INTERSECT
SELECT id FROM table2;
```

---

### 29. Update column based on another column

```sql
UPDATE employees
SET bonus = salary * 0.10;
```

---

### 30. Employees earning more than their manager

```sql
SELECT e.name
FROM employees e
JOIN employees m
ON e.manager_id = m.id
WHERE e.salary > m.salary;
```

---
Great 👍 Let’s cover **important SQL / Database theory concepts** that freshers are commonly asked — including **ACID properties**, transactions, constraints, etc. (Short and interview-ready answers.)

---

# 🔹 1. What are ACID Properties?

ACID ensures reliable database transactions.

### ✅ A – Atomicity

Transaction is **all or nothing**.
If one step fails → entire transaction rolls back.

### ✅ C – Consistency

Database moves from one **valid state to another**.
Rules, constraints are always maintained.

### ✅ I – Isolation

Multiple transactions don’t interfere with each other.

### ✅ D – Durability

Once committed, data is permanently saved (even after crash).

---

# 🔹 2. What is a Transaction?

A sequence of operations executed as a single unit.

```sql
BEGIN;
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;
COMMIT;
```

---

# 🔹 3. What is COMMIT?

Saves the transaction permanently.

```sql
COMMIT;
```

---

# 🔹 4. What is ROLLBACK?

Undoes changes in a transaction.

```sql
ROLLBACK;
```

---

# 🔹 5. What is SAVEPOINT?

Creates a checkpoint inside a transaction.

```sql
SAVEPOINT sp1;
ROLLBACK TO sp1;
```

---

# 🔹 6. What are Constraints?

Rules applied to columns to maintain data integrity.

### Types:

* NOT NULL
* UNIQUE
* PRIMARY KEY
* FOREIGN KEY
* CHECK
* DEFAULT

Example:

```sql
CREATE TABLE employees (
  id INT PRIMARY KEY,
  name VARCHAR(50) NOT NULL,
  salary INT CHECK (salary > 0)
);
```

---

# 🔹 7. What is a View?

A virtual table based on a query.

```sql
CREATE VIEW high_salary AS
SELECT name, salary
FROM employees
WHERE salary > 50000;
```

---

# 🔹 8. What is a Materialized View?

Stores query result physically (improves performance).
Needs manual refresh (in most DBs).

---

# 🔹 9. What is a Stored Procedure?

Precompiled SQL code stored in DB.

```sql
CREATE PROCEDURE getEmployees()
BEGIN
  SELECT * FROM employees;
END;
```

---

# 🔹 10. What is a Function?

Similar to procedure but **returns a value**.

---

# 🔹 11. What is a Trigger?

Automatically executes when an event occurs (INSERT, UPDATE, DELETE).

```sql
CREATE TRIGGER before_insert
BEFORE INSERT ON employees
FOR EACH ROW
SET NEW.created_at = NOW();
```

---

# 🔹 12. What is a Cursor?

Used to process rows one by one.

Used mainly in stored procedures.

---

# 🔹 13. What is a Deadlock?

When two transactions wait for each other to release locks.

DB automatically detects and kills one transaction.

---

# 🔹 14. What is Locking?

Mechanism to control concurrent access.

### Types:

* Shared Lock (Read)
* Exclusive Lock (Write)

---

# 🔹 15. What are Isolation Levels?

Defines how transactions are isolated.

1. Read Uncommitted
2. Read Committed
3. Repeatable Read
4. Serializable (Highest isolation)

---

# 🔹 16. What is Phantom Read?

When new rows appear during transaction re-execution.

---

# 🔹 17. What is Dirty Read?

Reading uncommitted data.

---

# 🔹 18. What is Non-Repeatable Read?

Row value changes between two reads in same transaction.

---

# 🔹 19. What is a Schema?

Logical container for database objects.

```sql
CREATE SCHEMA company;
```

---

# 🔹 20. What is Difference Between HAVING and GROUP BY?

* GROUP BY → groups rows
* HAVING → filters grouped results

---

# 🔹 21. What is a Self Join?

Joining a table with itself.

```sql
SELECT e.name, m.name AS manager
FROM employees e
JOIN employees m
ON e.manager_id = m.id;
```

---

# 🔹 22. What is a Composite Key?

Primary key made of multiple columns.

```sql
PRIMARY KEY (order_id, product_id)
```

---

# 🔹 23. What is Data Integrity?

Accuracy and consistency of data.

Types:

* Entity Integrity
* Referential Integrity
* Domain Integrity

---

# 🔹 24. What is the Difference Between OLTP and OLAP?

| OLTP                    | OLAP                    |
| ----------------------- | ----------------------- |
| Day-to-day transactions | Analytics               |
| Fast inserts/updates    | Complex queries         |
| Example: Banking system | Example: Data warehouse |

---

# 🔹 25. What is a Data Warehouse?

Centralized system for reporting and analytics.

---
