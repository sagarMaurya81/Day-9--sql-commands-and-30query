````markdown
# Day 9 — SQL Commands & Queries

## 📚 Overview

Day 9 focuses on basic SQL commands and business-oriented queries using PostgreSQL.

## 📝 Topics Covered

- SELECT
- INSERT
- UPDATE
- DELETE
- WHERE
- ORDER BY
- GROUP BY
- HAVING
- JOIN
- COUNT()
- SUM()
- AVG()
- MIN()
- MAX()

## 💻 Examples

### SELECT

```sql
SELECT *
FROM employee;
````

### INSERT

```sql
INSERT INTO employee
(first_name, last_name, email, salary)
VALUES
('Rahul', 'Sharma', 'rahul@example.com', 55000);
```

### UPDATE

```sql
UPDATE employee
SET salary = 60000
WHERE email = 'rahul@example.com';
```

### DELETE

```sql
DELETE FROM employee
WHERE email = 'rahul@example.com';
```

### WHERE

```sql
SELECT first_name, salary
FROM employee
WHERE salary > 60000;
```

### ORDER BY

```sql
SELECT first_name, salary
FROM employee
ORDER BY salary DESC;
```

### GROUP BY

```sql
SELECT department_id, COUNT(*) AS employee_count
FROM employee
GROUP BY department_id;
```

### HAVING

```sql
SELECT department_id, COUNT(*) AS employee_count
FROM employee
GROUP BY department_id
HAVING COUNT(*) > 5;
```

### JOIN

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

### Aggregate Functions

```sql
SELECT COUNT(*) FROM employee;

SELECT SUM(salary) FROM employee;

SELECT AVG(salary) FROM employee;

SELECT MIN(salary) FROM employee;

SELECT MAX(salary) FROM employee;
```

## 💼 Business Queries

### Highest-paid employee

```sql
SELECT first_name, last_name, salary
FROM employee
ORDER BY salary DESC
LIMIT 1;
```

### Average salary by department

```sql
SELECT
    d.department_name,
    AVG(e.salary) AS average_salary
FROM employee e
JOIN department d
    ON e.department_id = d.department_id
GROUP BY d.department_name;
```

### Total salary expense

```sql
SELECT SUM(salary) AS total_salary
FROM employee;
```

### Employees with salary above ₹70,000

```sql
SELECT first_name, last_name, salary
FROM employee
WHERE salary > 70000;
```

## ✅ Key Takeaway

SQL is used not only to manage database data but also to answer real **business questions** using filtering, grouping, joins, and aggregate functions.

```
```
