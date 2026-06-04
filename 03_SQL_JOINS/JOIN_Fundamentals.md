# JOINS IN SQL

## 1. What is a JOIN?

A JOIN is used to combine data from two or more tables based on a related column between them.

It allows us to retrieve information that is stored across multiple tables.

---

## 2. Why Do We Need JOINs?

In real-world databases, data is usually divided into multiple tables to avoid duplication and improve maintainability.

This process is called **Database Normalization**.

### Example

### Employees Table

| employee_id | employee_name | department_id |
| ----------- | ------------- | ------------- |
| 1           | John          | 101           |
| 2           | Alice         | 102           |
| 3           | Bob           | 101           |

---

### Departments Table

| department_id | department_name |
| ------------- | --------------- |
| 101           | IT              |
| 102           | HR              |

---

Suppose we want:

```text
Employee Name + Department Name
```

Employee name is in:

```text
Employees
```

Department name is in:

```text
Departments
```

To combine them, we use JOIN.

---

## 3. Problem Without JOIN

Employees Table:

| employee_id | employee_name | department_id |
| ----------- | ------------- | ------------- |
| 1           | John          | 101           |

Departments Table:

| department_id | department_name |
| ------------- | --------------- |
| 101           | IT              |

Without JOIN:

```sql
SELECT *
FROM Employees;
```

Output:

| employee_name | department_id |
| ------------- | ------------- |
| John          | 101           |

We cannot see:

```text
IT
```

because it exists in another table.

JOIN solves this problem.

---

## 4. What is a Primary Key?

A Primary Key uniquely identifies each row in a table.

Example:

```text
employee_id
```

No duplicates allowed.

---

## 5. What is a Foreign Key?

A Foreign Key is a column that refers to a Primary Key in another table.

Example:

Employees Table

| employee_id | department_id |
| ----------- | ------------- |
| 1           | 101           |

Departments Table

| department_id |
| ------------- |
| 101           |

Here:

```text
department_id
```

in Employees is a Foreign Key.

---

## 6. How JOIN Works

### Table 1

| id | name  |
| -- | ----- |
| 1  | John  |
| 2  | Alice |

---

### Table 2

| id | city   |
| -- | ------ |
| 1  | Pune   |
| 2  | Mumbai |

---

Query:

```sql
SELECT *
FROM Table1
JOIN Table2
ON Table1.id = Table2.id;
```

Output:

| id | name  | city   |
| -- | ----- | ------ |
| 1  | John  | Pune   |
| 2  | Alice | Mumbai |

---

## 7. General JOIN Syntax

```sql
SELECT columns
FROM table1
JOIN table2
ON table1.common_column = table2.common_column;
```

---

Using aliases:

```sql
SELECT t1.column_name,
       t2.column_name
FROM table1 t1
JOIN table2 t2
ON t1.id = t2.id;
```

---

## 8. Types of JOINs

SQL provides several types of joins.

### 1. INNER JOIN

Returns only matching rows.

```sql
SELECT *
FROM table1
INNER JOIN table2
ON table1.id = table2.id;
```

---

### 2. LEFT JOIN

Returns:

* All rows from left table
* Matching rows from right table

```sql
SELECT *
FROM table1
LEFT JOIN table2
ON table1.id = table2.id;
```

---

### 3. RIGHT JOIN

Returns:

* All rows from right table
* Matching rows from left table

```sql
SELECT *
FROM table1
RIGHT JOIN table2
ON table1.id = table2.id;
```

---

### 4. FULL OUTER JOIN

Returns:

* All matching rows
* All unmatched rows from left table
* All unmatched rows from right table

```sql
SELECT *
FROM table1
FULL OUTER JOIN table2m
ON table1.id = table2.id;
```

---

### 5. SELF JOIN

A table joined with itself.

```sql
SELECT *
FROM Employees e1
JOIN Employees e2
ON e1.manager_id = e2.employee_id;
```

Used for hierarchical data.

---

### 6. CROSS JOIN

Returns Cartesian Product.

Every row from first table combines with every row from second table.

```sql
SELECT *
FROM table1
CROSS JOIN table2;
```

If:

```text
Table1 = 3 rows
Table2 = 4 rows
```

Result:

```text
3 × 4 = 12 rows
```

---

## 9. JOIN Diagram Summary

### INNER JOIN

```text
Only Matching Rows
```

---

### LEFT JOIN

```text
All Left + Matching Right
```

---

### RIGHT JOIN

```text
All Right + Matching Left
```

---

### FULL OUTER JOIN

```text
Everything from Both Tables
```

---

### SELF JOIN

```text
Table Joined with Itself
```

---

### CROSS JOIN

```text
Every Combination Possible
```

---

## 10. Multiple Table JOIN

We can join more than two tables.

Example:

Employees

↓

Departments

↓

Locations

```sql
SELECT e.employee_name,
       d.department_name,
       l.city
FROM Employees e
JOIN Departments d
ON e.department_id = d.department_id
JOIN Locations l
ON d.location_id = l.location_id;
```

---

## 11. Order of Execution

Query:

```sql
SELECT *
FROM Employees e
JOIN Departments d
ON e.department_id = d.department_id
WHERE salary > 50000;
```

Execution Order:

```text
1. FROM
2. JOIN
3. ON
4. WHERE
5. GROUP BY
6. HAVING
7. SELECT
8. ORDER BY
9. LIMIT
```

Interview favorite.

---

## 12. Real World Use Cases

### E-Commerce

Products + Categories

```sql
Products
JOIN Categories
```

---

### Banking

Customers + Accounts

```sql
Customers
JOIN Accounts
```

---

### College

Students + Courses

```sql
Students
JOIN Courses
```

---

### Company

Employees + Departments

```sql
Employees
JOIN Departments
```

---

## 13. Common Mistakes

### Mistake 1

Missing ON Condition

Wrong:

```sql
SELECT *
FROM Employees
JOIN Departments;
```

---

### Mistake 2

Joining Wrong Columns

Wrong:

```sql
ON employee_id = department_id
```

---

### Mistake 3

Using SELECT *

When many columns exist.

Prefer:

```sql
SELECT employee_name,
       department_name
```

---

### Mistake 4

Confusing LEFT JOIN and INNER JOIN

Remember:

```text
INNER JOIN → Only Matches
LEFT JOIN  → All Left Rows
```

---

## 14. Interview Questions

### Q1. What is a JOIN?

Answer:

A JOIN combines rows from multiple tables based on a related column.

---

### Q2. Why Do We Need JOINs?

Answer:

Data is stored across multiple tables due to normalization.

JOIN combines related data.

---

### Q3. Most Commonly Used JOIN?

Answer:

```sql
INNER JOIN
```

and

```sql
LEFT JOIN
```

---

### Q4. Difference Between INNER JOIN and LEFT JOIN?

| INNER JOIN                 | LEFT JOIN                                     |
| -------------------------- | --------------------------------------------- |
| Returns matching rows only | Returns all left rows and matching right rows |

---

### Q5. What is a Foreign Key?

Answer:

A column that references the Primary Key of another table.

---

## 15. Key Takeaways

* JOIN combines data from multiple tables.
* JOIN works using related columns.
* Primary Key uniquely identifies rows.
* Foreign Key creates relationships.
* INNER JOIN returns matching rows.
* LEFT JOIN returns all left rows.
* RIGHT JOIN returns all right rows.
* FULL OUTER JOIN returns everything.
* SELF JOIN joins a table with itself.
* CROSS JOIN creates all possible combinations.

---

## 16. Revision Notes

```sql
SELECT *
FROM table1
INNER JOIN table2
ON table1.id = table2.id;
```

```sql
SELECT *
FROM table1
LEFT JOIN table2
ON table1.id = table2.id;
```

```sql
SELECT *
FROM table1
RIGHT JOIN table2
ON table1.id = table2.id;
```

```sql
SELECT *
FROM table1
FULL OUTER JOIN table2
ON table1.id = table2.id;
```

```sql
SELECT *
FROM table1
CROSS JOIN table2;
```

```sql
SELECT *
FROM Employees e1
JOIN Employees e2
ON e1.manager_id = e2.employee_id;
```

---

## 17. My Learning

Date: __________

Topic: JOINS

### What I Learned

* Why joins are needed.
* Primary Key and Foreign Key concepts.
* How tables are related.
* Types of joins.
* General join syntax.
* Real-world use cases.

Confidence: ____ / 10
Difficulty: __________
