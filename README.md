````markdown
# Day 9 — SQL Commands & Business Queries

## 📚 Overview

**Day 9** focuses on SQL commands used to create, read, update, delete, filter, sort, group, aggregate, and join data in PostgreSQL.

The examples use an **Employee Management System** with tables such as `employee`, `department`, `designation`, and `manager`.

## 🎯 Learning Objectives

By the end of Day 9, you will understand how to:

- Retrieve data using `SELECT`
- Add data using `INSERT`
- Modify data using `UPDATE`
- Remove data using `DELETE`
- Filter records using `WHERE`
- Sort records using `ORDER BY`
- Group records using `GROUP BY`
- Filter groups using `HAVING`
- Combine tables using `JOIN`
- Calculate business metrics using `COUNT`, `SUM`, `AVG`, `MIN`, and `MAX`
- Write SQL queries that answer **business questions**, not only database questions

---

## 🗂️ SQL Commands Covered

| Command / Topic | Purpose |
|---|---|
| `SELECT` | Retrieve data from a table |
| `INSERT` | Add new records |
| `UPDATE` | Modify existing records |
| `DELETE` | Remove records |
| `WHERE` | Filter rows |
| `ORDER BY` | Sort results |
| `GROUP BY` | Create groups for aggregate calculations |
| `HAVING` | Filter grouped results |
| `JOIN` | Combine related tables |
| `COUNT()` | Count rows |
| `SUM()` | Calculate total |
| `AVG()` | Calculate average value |
| `MIN()` | Find minimum value |
| `MAX()` | Find maximum value |

---

# 1. SELECT

Used to retrieve data from a table.

```sql
-- Get all employees
SELECT *
FROM employee;
````

### Example

```sql
SELECT first_name, last_name, email, salary
FROM employee;
```

![SELECT Example](images/01-select.png)

---

# 2. INSERT

Used to insert a new record into a table.

```sql
INSERT INTO employee
(first_name, last_name, email, salary, department_id, designation_id, manager_id)
VALUES
('Rahul', 'Sharma', 'rahul@example.com', 55000, 1, 2, 1);
```

![INSERT Example](images/02-insert.png)

---

# 3. UPDATE

Used to modify existing records.

```sql
UPDATE employee
SET salary = 60000
WHERE email = 'rahul@example.com';
```

![UPDATE Example](images/03-update.png)

> ⚠️ Always use a suitable `WHERE` condition with `UPDATE` unless you intentionally want to update every row.

---

# 4. DELETE

Used to remove records.

```sql
DELETE FROM employee
WHERE email = 'rahul@example.com';
```

![DELETE Example](images/04-delete.png)

> ⚠️ Always verify the `WHERE` condition before running `DELETE`.

---

# 5. WHERE

Used to filter rows based on a condition.

```sql
-- Employees with salary greater than 60000
SELECT first_name, last_name, salary
FROM employee
WHERE salary > 60000;
```

![WHERE Example](images/05-where.png)

---

# 6. ORDER BY

Used to sort query results in ascending (`ASC`) or descending (`DESC`) order.

```sql
-- Highest-paid employees first
SELECT first_name, last_name, salary
FROM employee
ORDER BY salary DESC;
```

![ORDER BY Example](images/06-order-by.png)

---

# 7. GROUP BY

Used to group rows so aggregate functions can be applied to each group.

```sql
-- Number of employees in each department
SELECT department_id, COUNT(*) AS employee_count
FROM employee
GROUP BY department_id;
```

![GROUP BY Example](images/07-group-by.png)

---

# 8. HAVING

Used to filter grouped results.

`WHERE` filters rows **before grouping**, while `HAVING` filters groups **after grouping**.

```sql
-- Departments having more than 3 employees
SELECT department_id, COUNT(*) AS employee_count
FROM employee
GROUP BY department_id
HAVING COUNT(*) > 3;
```

![HAVING Example](images/08-having.png)

---

# 9. JOIN

`JOIN` is used to combine data from related tables.

### INNER JOIN Example

```sql
SELECT
    e.first_name,
    e.last_name,
    d.department_name,
    e.salary
FROM employee e
JOIN department d
    ON e.department_id = d.department_id;
```

![JOIN Example](images/09-join.png)

### Common JOIN Types

| JOIN              | Meaning                                                               |
| ----------------- | --------------------------------------------------------------------- |
| `INNER JOIN`      | Returns matching rows from both tables                                |
| `LEFT JOIN`       | Returns all rows from the left table and matching rows from the right |
| `RIGHT JOIN`      | Returns all rows from the right table and matching rows from the left |
| `FULL OUTER JOIN` | Returns all rows from both tables                                     |
| `CROSS JOIN`      | Returns every possible combination of rows                            |

---

# 10. COUNT()

Counts rows or non-NULL values.

```sql
SELECT COUNT(*) AS total_employees
FROM employee;
```

![COUNT Example](images/10-count.png)

---

# 11. SUM()

Calculates the total of a numeric column.

```sql
SELECT SUM(salary) AS total_salary
FROM employee;
```

![SUM Example](images/11-sum.png)

---

# 12. AVG()

Calculates the average value.

```sql
SELECT AVG(salary) AS average_salary
FROM employee;
```

![AVG Example](images/12-avg.png)

---

# 13. MIN()

Returns the smallest value.

```sql
SELECT MIN(salary) AS lowest_salary
FROM employee;
```

![MIN Example](images/13-min.png)

---

# 14. MAX()

Returns the largest value.

```sql
SELECT MAX(salary) AS highest_salary
FROM employee;
```

![MAX Example](images/14-max.png)

---

# 💼 Business Questions & SQL Queries

The goal is to write queries that help a company make decisions.

## 1. Which employees earn more than ₹70,000?

```sql
SELECT first_name, last_name, salary
FROM employee
WHERE salary > 70000
ORDER BY salary DESC;
```

## 2. What is the total salary expense of the company?

```sql
SELECT SUM(salary) AS total_salary_expense
FROM employee;
```

## 3. What is the average salary by department?

```sql
SELECT
    d.department_name,
    ROUND(AVG(e.salary), 2) AS average_salary
FROM employee e
JOIN department d
    ON e.department_id = d.department_id
GROUP BY d.department_name
ORDER BY average_salary DESC;
```

![Business Query Example](images/15-business-query.png)

## 4. Which departments have more than 5 employees?

```sql
SELECT
    d.department_name,
    COUNT(e.employee_id) AS employee_count
FROM employee e
JOIN department d
    ON e.department_id = d.department_id
GROUP BY d.department_name
HAVING COUNT(e.employee_id) > 5;
```

## 5. Who is the highest-paid employee?

```sql
SELECT first_name, last_name, salary
FROM employee
ORDER BY salary DESC
LIMIT 1;
```

## 6. What is the salary range?

```sql
SELECT
    MIN(salary) AS lowest_salary,
    MAX(salary) AS highest_salary
FROM employee;
```

---

# 🧠 SQL Query Pattern

A common reporting query follows this pattern:

```sql
SELECT column1, aggregate_function(column2)
FROM table_name
JOIN another_table
    ON table_name.id = another_table.id
WHERE condition
GROUP BY column1
HAVING aggregate_condition
ORDER BY column1;
```

### Logical Processing Order

```text
FROM / JOIN
     ↓
WHERE
     ↓
GROUP BY
     ↓
HAVING
     ↓
SELECT
     ↓
ORDER BY
```

---

# 🛠️ PostgreSQL Setup

Open the PostgreSQL shell:

```bash
psql -U postgres
```

Connect to your database:

```sql
\c employee_management
```

Check available tables:

```sql
\dt
```

View table structure:

```sql
\d employee
```

---

# 📌 Practical Task

Design and query an **Employee Management System** using these entities:

```text
Employee
Department
Designation
Manager
```

Write SQL queries to answer real business questions such as:

* Which department has the highest average salary?
* How many employees are in each department?
* Which employee has the highest salary?
* What is the total salary expense?
* Which departments have more than a given number of employees?
* Which employees belong to the IT department?

---

# ✅ Day 9 Summary

You learned how to use SQL for both **database operations** and **business reporting**.

The most important concepts covered are:

`SELECT` → `INSERT` → `UPDATE` → `DELETE` → `WHERE` → `ORDER BY` → `GROUP BY` → `HAVING` → `JOIN` → `COUNT` → `SUM` → `AVG` → `MIN` → `MAX`

> **Key takeaway:** Good SQL is not only about retrieving data. It is about answering useful business questions from data.

```
```
