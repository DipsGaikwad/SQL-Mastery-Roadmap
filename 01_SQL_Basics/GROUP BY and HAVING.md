# GROUP BY and HAVING

## 1. Definition

### GROUP BY

The `GROUP BY` clause is used to group rows that have the same values in specified columns.

It is commonly used with aggregate functions such as:

* COUNT()
* SUM()
* AVG()
* MIN()
* MAX()

---

### HAVING

The `HAVING` clause is used to filter groups after the grouping operation has been performed.

Think of it as:

```text
WHERE  → Filters rows
HAVING → Filters groups
```

---

## 2. Why Do We Need GROUP BY?

Consider the following Employees table:

| employee_id | department | salary |
| ----------- | ---------- | ------ |
| 1           | IT         | 50000  |
| 2           | IT         | 60000  |
| 3           | HR         | 45000  |
| 4           | HR         | 55000  |
| 5           | Sales      | 70000  |

Business Questions:

* How many employees are in each department?
* What is the total salary per department?
* What is the average salary per department?
* Which departments have more than one employee?

These questions cannot be answered efficiently without GROUP BY.

---

## 3. GROUP BY Syntax

```sql
SELECT column_name,
       aggregate_function(column_name)
FROM table_name
GROUP BY column_name;
```

Example:

```sql
SELECT department,
       COUNT(*)
FROM Employees
GROUP BY department;
```

---

## 4. How GROUP BY Works

Table:

| employee_id | department |
| ----------- | ---------- |
| 1           | IT         |
| 2           | IT         |
| 3           | HR         |
| 4           | HR         |
| 5           | Sales      |

Query:

```sql
SELECT department,
       COUNT(*)
FROM Employees
GROUP BY department;
```

Output:

| department | COUNT(*) |
| ---------- | -------- |
| IT         | 2        |
| HR         | 2        |
| Sales      | 1        |

GROUP BY creates separate groups and then applies the aggregate function to each group.

---

## 5. GROUP BY with COUNT()

### Count Employees per Department

```sql
SELECT department,
       COUNT(*)
FROM Employees
GROUP BY department;
```

Output:

| department | employee_count |
| ---------- | -------------- |
| IT         | 2              |
| HR         | 2              |
| Sales      | 1              |

---

## 6. GROUP BY with SUM()

### Total Salary per Department

```sql
SELECT department,
       SUM(salary)
FROM Employees
GROUP BY department;
```

Output:

| department | total_salary |
| ---------- | ------------ |
| IT         | 110000       |
| HR         | 100000       |
| Sales      | 70000        |

---

## 7. GROUP BY with AVG()

### Average Salary per Department

```sql
SELECT department,
       AVG(salary)
FROM Employees
GROUP BY department;
```

Output:

| department | avg_salary |
| ---------- | ---------- |
| IT         | 55000      |
| HR         | 50000      |
| Sales      | 70000      |

---

## 8. GROUP BY with MAX()

### Highest Salary in Each Department

```sql
SELECT department,
       MAX(salary)
FROM Employees
GROUP BY department;
```

---

## 9. GROUP BY with MIN()

### Lowest Salary in Each Department

```sql
SELECT department,
       MIN(salary)
FROM Employees
GROUP BY department;
```

---

## 10. Multiple Column GROUP BY

Example:

| employee_id | department | city   |
| ----------- | ---------- | ------ |
| 1           | IT         | Mumbai |
| 2           | IT         | Pune   |
| 3           | HR         | Mumbai |

Query:

```sql
SELECT department,
       city,
       COUNT(*)
FROM Employees
GROUP BY department, city;
```

Output:

Groups are formed based on both department and city.

---

## 11. HAVING Clause

### Definition

HAVING filters grouped data.

Syntax:

```sql
SELECT column_name,
       aggregate_function(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

---

## 12. Why HAVING Is Needed

Suppose we want only departments having more than one employee.

Query:

```sql
SELECT department,
       COUNT(*)
FROM Employees
GROUP BY department
HAVING COUNT(*) > 1;
```

Output:

| department | COUNT(*) |
| ---------- | -------- |
| IT         | 2        |
| HR         | 2        |

Sales is removed because it contains only one employee.

---

## 13. WHERE vs HAVING

### WHERE

Filters rows before grouping.

```sql
SELECT *
FROM Employees
WHERE salary > 50000;
```

---

### HAVING

Filters groups after grouping.

```sql
SELECT department,
       COUNT(*)
FROM Employees
GROUP BY department
HAVING COUNT(*) > 1;
```

---

## 14. WHERE + GROUP BY + HAVING

Example:

```sql
SELECT department,
       AVG(salary)
FROM Employees
WHERE salary > 45000
GROUP BY department
HAVING AVG(salary) > 55000;
```

Execution:

1. WHERE filters rows
2. GROUP BY creates groups
3. AVG() calculates averages
4. HAVING filters groups
5. SELECT returns results

---

## 15. SQL Execution Order

Query:

```sql
SELECT department,
       COUNT(*)
FROM Employees
WHERE salary > 50000
GROUP BY department
HAVING COUNT(*) > 1
ORDER BY department;
```

Actual Execution Order:

```text
1. FROM
2. WHERE
3. GROUP BY
4. HAVING
5. SELECT
6. ORDER BY
```

This is a very common interview question.

---

## 16. Common Mistakes

### Mistake 1

Wrong:

```sql
SELECT department,
       salary
FROM Employees
GROUP BY department;
```

Reason:

salary is neither:

* grouped
* nor aggregated

Most databases will throw an error.

---

Correct:

```sql
SELECT department,
       AVG(salary)
FROM Employees
GROUP BY department;
```

---

### Mistake 2

Using WHERE with Aggregate Functions

Wrong:

```sql
SELECT department,
       COUNT(*)
FROM Employees
WHERE COUNT(*) > 1
GROUP BY department;
```

---

Correct:

```sql
SELECT department,
       COUNT(*)
FROM Employees
GROUP BY department
HAVING COUNT(*) > 1;
```

---

### Mistake 3

Forgetting GROUP BY

Wrong:

```sql
SELECT department,
       COUNT(*)
FROM Employees;
```

May result in an error because department is not grouped.

---

Correct:

```sql
SELECT department,
       COUNT(*)
FROM Employees
GROUP BY department;
```

---

## 17. Real World Use Cases

### Number of Orders per Customer

```sql
SELECT customer_id,
       COUNT(*)
FROM Orders
GROUP BY customer_id;
```

---

### Total Sales per Product

```sql
SELECT product_id,
       SUM(amount)
FROM Sales
GROUP BY product_id;
```

---

### Average Rating per Movie

```sql
SELECT movie_id,
       AVG(rating)
FROM Reviews
GROUP BY movie_id;
```

---

### Departments Having More Than 10 Employees

```sql
SELECT department,
       COUNT(*)
FROM Employees
GROUP BY department
HAVING COUNT(*) > 10;
```

---

## 18. Interview Questions

### Q1. Difference Between WHERE and HAVING?

Answer:

| WHERE                    | HAVING                  |
| ------------------------ | ----------------------- |
| Filters rows             | Filters groups          |
| Executes before GROUP BY | Executes after GROUP BY |

---

### Q2. Can HAVING Be Used Without GROUP BY?

Yes.

```sql
SELECT COUNT(*)
FROM Employees
HAVING COUNT(*) > 5;
```

Though uncommon, it is valid SQL.

---

### Q3. Can GROUP BY Be Used Without Aggregate Functions?

Yes.

```sql
SELECT department
FROM Employees
GROUP BY department;
```

Equivalent to:

```sql
SELECT DISTINCT department
FROM Employees;
```

---

### Q4. Which Executes First: WHERE or HAVING?

Answer:

```text
WHERE executes first.
HAVING executes after GROUP BY.
```

---

### Q5. Why Do We Need HAVING?

Because aggregate functions cannot be used inside WHERE.

Wrong:

```sql
WHERE COUNT(*) > 5
```

Correct:

```sql
HAVING COUNT(*) > 5
```

---

## 19. Hands-On Practice

### Practice 1

Count employees per department.

```sql
SELECT department,
       COUNT(*)
FROM Employees
GROUP BY department;
```

---

### Practice 2

Calculate total salary per department.

```sql
SELECT department,
       SUM(salary)
FROM Employees
GROUP BY department;
```

---

### Practice 3

Find average salary per department.

```sql
SELECT department,
       AVG(salary)
FROM Employees
GROUP BY department;
```

---

### Practice 4

Find departments with more than 2 employees.

```sql
SELECT department,
       COUNT(*)
FROM Employees
GROUP BY department
HAVING COUNT(*) > 2;
```

---

### Practice 5

Find departments where average salary exceeds 60000.

```sql
SELECT department,
       AVG(salary)
FROM Employees
GROUP BY department
HAVING AVG(salary) > 60000;
```

---

## 20. Key Takeaways

* GROUP BY creates groups.
* Aggregate functions are usually used with GROUP BY.
* HAVING filters grouped data.
* WHERE filters rows.
* HAVING filters groups.
* GROUP BY is one of the most important SQL interview topics.
* Many LeetCode SQL questions use GROUP BY + HAVING.

---

## 21. Revision Notes

```sql
SELECT department,
       COUNT(*)
FROM Employees
GROUP BY department;
```

```sql
SELECT department,
       SUM(salary)
FROM Employees
GROUP BY department;
```

```sql
SELECT department,
       AVG(salary)
FROM Employees
GROUP BY department;
```

```sql
SELECT department,
       COUNT(*)
FROM Employees
GROUP BY department
HAVING COUNT(*) > 1;
```

```sql
SELECT department,
       AVG(salary)
FROM Employees
GROUP BY department
HAVING AVG(salary) > 50000;
```

---

## 22. My Learning

Date: __________

Topic: GROUP BY and HAVING

### What I Learned

* GROUP BY creates groups of rows.
* Aggregate functions work on groups.
* HAVING filters grouped data.
* WHERE filters rows before grouping.
* HAVING filters groups after grouping.
* GROUP BY + HAVING is heavily used in SQL interviews.

Difficulty Level: __________

Confidence: ____ / 10
