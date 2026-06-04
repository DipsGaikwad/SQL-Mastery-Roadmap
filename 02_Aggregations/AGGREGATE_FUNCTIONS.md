# Aggregate Functions

## 1. Definition

Aggregate Functions are SQL functions that perform calculations on multiple rows and return a single summarized result.

They are commonly used to:

- Count records
- Calculate totals
- Find averages
- Find minimum values
- Find maximum values

---

## 2. Why Do We Need Aggregate Functions?

Consider the following Employees table:

| employee_id | employee_name | salary |
|------------|--------------|---------|
| 1 | John | 50000 |
| 2 | Alice | 60000 |
| 3 | Bob | 70000 |
| 4 | David | 80000 |

Business questions:

- How many employees are there?
- What is the total salary?
- What is the average salary?
- What is the highest salary?
- What is the lowest salary?

Aggregate functions help answer these questions.

---

## 3. Aggregate Functions Overview

| Function | Purpose |
|----------|---------|
| COUNT() | Counts rows |
| SUM() | Adds values |
| AVG() | Calculates average |
| MIN() | Finds smallest value |
| MAX() | Finds largest value |

---

# 4. COUNT()

## Definition

The `COUNT()` function returns the number of rows.

## Syntax

```sql
SELECT COUNT(*)
FROM table_name;
```

## Example

```sql
SELECT COUNT(*)
FROM Employees;
```

Output:

| COUNT(*) |
|----------|
| 4 |

---

## COUNT(column_name)

```sql
SELECT COUNT(salary)
FROM Employees;
```

Counts only non-NULL salary values.

---

## Real World Use Cases

### Count Total Employees

```sql
SELECT COUNT(*)
FROM Employees;
```

### Count Total Customers

```sql
SELECT COUNT(*)
FROM Customers;
```

---

# 5. SUM()

## Definition

The `SUM()` function returns the total of a numeric column.

## Syntax

```sql
SELECT SUM(column_name)
FROM table_name;
```

## Example

```sql
SELECT SUM(salary)
FROM Employees;
```

Output:

| SUM(salary) |
|------------|
| 260000 |

---

## Real World Use Cases

### Calculate Total Sales

```sql
SELECT SUM(amount)
FROM Orders;
```

### Calculate Total Revenue

```sql
SELECT SUM(revenue)
FROM Sales;
```

---

# 6. AVG()

## Definition

The `AVG()` function calculates the average value.

## Syntax

```sql
SELECT AVG(column_name)
FROM table_name;
```

## Example

```sql
SELECT AVG(salary)
FROM Employees;
```

Output:

| AVG(salary) |
|------------|
| 65000 |

---

## Real World Use Cases

### Average Salary

```sql
SELECT AVG(salary)
FROM Employees;
```

### Average Product Price

```sql
SELECT AVG(price)
FROM Products;
```

---

# 7. MIN()

## Definition

The `MIN()` function returns the smallest value.

## Syntax

```sql
SELECT MIN(column_name)
FROM table_name;
```

## Example

```sql
SELECT MIN(salary)
FROM Employees;
```

Output:

| MIN(salary) |
|------------|
| 50000 |

---

## Real World Use Cases

### Lowest Salary

```sql
SELECT MIN(salary)
FROM Employees;
```

### Cheapest Product

```sql
SELECT MIN(price)
FROM Products;
```

---

# 8. MAX()

## Definition

The `MAX()` function returns the largest value.

## Syntax

```sql
SELECT MAX(column_name)
FROM table_name;
```

## Example

```sql
SELECT MAX(salary)
FROM Employees;
```

Output:

| MAX(salary) |
|------------|
| 80000 |

---

## Real World Use Cases

### Highest Salary

```sql
SELECT MAX(salary)
FROM Employees;
```

### Most Expensive Product

```sql
SELECT MAX(price)
FROM Products;
```

---

# 9. Aggregate Functions with WHERE

Aggregate functions can be combined with WHERE.

Example:

```sql
SELECT AVG(salary)
FROM Employees
WHERE salary > 50000;
```

Explanation:

- First filters rows
- Then calculates average

---

# 10. Handling NULL Values

Aggregate functions ignore NULL values.

Example:

| salary |
|---------|
| 50000 |
| NULL |
| 70000 |

Query:

```sql
SELECT AVG(salary)
FROM Employees;
```

Result:

```text
(50000 + 70000) / 2
```

NULL is ignored.

---

# 11. Common Mistakes

## Mistake 1

Wrong:

```sql
SELECT SUM(employee_name)
FROM Employees;
```

Reason:

SUM works only on numeric columns.

---

## Mistake 2

Confusing COUNT(*) and COUNT(column)

```sql
COUNT(*)
```

Counts all rows.

```sql
COUNT(column_name)
```

Counts only non-NULL values.

---

## Mistake 3

Using Aggregate Functions Without Understanding NULL

Remember:

```sql
AVG()
SUM()
MIN()
MAX()
COUNT(column)
```

ignore NULL values.

---

# 12. Interview Questions

## Q1. Difference Between COUNT(*) and COUNT(column)?

Answer:

```sql
COUNT(*)
```

Counts all rows.

```sql
COUNT(column_name)
```

Counts only non-NULL values.

---

## Q2. Which Aggregate Functions Ignore NULL Values?

Answer:

- COUNT(column)
- SUM()
- AVG()
- MIN()
- MAX()

All ignore NULL values.

---

## Q3. Can Aggregate Functions Be Used with WHERE?

Yes.

Example:

```sql
SELECT AVG(salary)
FROM Employees
WHERE department = 'IT';
```

---

## Q4. Which Aggregate Function Returns the Largest Value?

Answer:

```sql
MAX()
```

---

## Q5. Which Aggregate Function Returns the Smallest Value?

Answer:

```sql
MIN()
```

---

# 13. Hands-On Practice

### Practice 1

Count employees.

```sql
SELECT COUNT(*)
FROM Employees;
```

### Practice 2

Calculate total salary.

```sql
SELECT SUM(salary)
FROM Employees;
```

### Practice 3

Find average salary.

```sql
SELECT AVG(salary)
FROM Employees;
```

### Practice 4

Find highest salary.

```sql
SELECT MAX(salary)
FROM Employees;
```

### Practice 5

Find lowest salary.

```sql
SELECT MIN(salary)
FROM Employees;
```

---

# 14. Key Takeaways

- Aggregate functions summarize data.
- COUNT() counts rows.
- SUM() calculates totals.
- AVG() calculates averages.
- MIN() finds the smallest value.
- MAX() finds the largest value.
- Aggregate functions ignore NULL values.
- Aggregate functions are heavily used in reporting and analytics.

---

# 15. Revision Notes

```sql
SELECT COUNT(*)
FROM table_name;
```

```sql
SELECT SUM(column_name)
FROM table_name;
```

```sql
SELECT AVG(column_name)
FROM table_name;
```

```sql
SELECT MIN(column_name)
FROM table_name;
```

```sql
SELECT MAX(column_name)
FROM table_name;
```

---

# 16. My Learning

**Date:** __________

**Topic:** Aggregate Functions

### What I Learned

- COUNT() counts rows.
- SUM() calculates totals.
- AVG() calculates averages.
- MIN() finds smallest value.
- MAX() finds largest value.
- Aggregate functions ignore NULL values.

**Difficulty Level:** __________

**Confidence:** ____ / 10