# WHERE Clause (Numeric Filtering)

## 1. Definition

The `WHERE` clause is used to filter rows from a table based on a specified condition.

Instead of returning all rows from a table, SQL returns only the rows that satisfy the condition.

Without a WHERE clause, all rows are returned.

---

## 2. Why Do We Need WHERE?

Imagine a table contains 1,000,000 movie records.

If you only need movies released after 2010, retrieving every row would be inefficient.

The WHERE clause helps:

* Reduce unnecessary data
* Improve query performance
* Return only relevant results

Example:

```sql
SELECT *
FROM movies
WHERE year > 2010;
```

---

## 3. Syntax

### Basic Syntax

```sql
SELECT column_name
FROM table_name
WHERE condition;
```

### Multiple Conditions

```sql
SELECT column_name
FROM table_name
WHERE condition1
AND condition2;
```

```sql
SELECT column_name
FROM table_name
WHERE condition1
OR condition2;
```

---

## 4. SQL Query Execution Order

Although we write:

```sql
SELECT title
FROM movies
WHERE year > 2000;
```

SQL processes it internally as:

1. FROM
2. WHERE
3. SELECT

### Example

```sql
SELECT title
FROM movies
WHERE year > 2000;
```

Step 1:

```sql
FROM movies
```

Read all rows.

Step 2:

```sql
WHERE year > 2000
```

Filter matching rows.

Step 3:

```sql
SELECT title
```

Return only the title column.

---

## 5. Numeric Operators

| Operator | Meaning                  | Example      |
| -------- | ------------------------ | ------------ |
| =        | Equal To                 | year = 2000  |
| !=       | Not Equal To             | year != 2000 |
| <>       | Not Equal To             | year <> 2000 |
| >        | Greater Than             | year > 2000  |
| <        | Less Than                | year < 2000  |
| >=       | Greater Than or Equal To | year >= 2000 |
| <=       | Less Than or Equal To    | year <= 2000 |

---

## 6. Range Operators

### BETWEEN

Checks whether a value lies within a range.

```sql
SELECT *
FROM movies
WHERE year BETWEEN 2000 AND 2010;
```

Equivalent to:

```sql
SELECT *
FROM movies
WHERE year >= 2000
AND year <= 2010;
```

---

### NOT BETWEEN

```sql
SELECT *
FROM movies
WHERE year NOT BETWEEN 2000 AND 2010;
```

Returns rows outside the specified range.

---

## 7. List Operators

### IN

Checks whether a value exists in a list.

```sql
SELECT *
FROM movies
WHERE year IN (1995, 2000, 2010);
```

Equivalent to:

```sql
SELECT *
FROM movies
WHERE year = 1995
OR year = 2000
OR year = 2010;
```

---

### NOT IN

```sql
SELECT *
FROM movies
WHERE year NOT IN (1995, 2000, 2010);
```

---

## 8. Sample Data

| id | title        | year |
| -- | ------------ | ---- |
| 1  | Toy Story    | 1995 |
| 5  | Finding Nemo | 2003 |
| 7  | Cars         | 2006 |
| 11 | Toy Story 3  | 2010 |
| 13 | Brave        | 2012 |

---

## 9. SQLBolt Exercise Solutions

### Task 1: Find the Movie with Row ID = 6

```sql
SELECT *
FROM movies
WHERE id = 6;
```

Output:

| id | title           |
| -- | --------------- |
| 6  | The Incredibles |

---

### Task 2: Find Movies Released Between 2000 and 2010

```sql
SELECT *
FROM movies
WHERE year BETWEEN 2000 AND 2010;
```

Alternative:

```sql
SELECT *
FROM movies
WHERE year >= 2000
AND year <= 2010;
```

---

### Task 3: Find Movies Not Released Between 2000 and 2010

```sql
SELECT *
FROM movies
WHERE year NOT BETWEEN 2000 AND 2010;
```

Alternative:

```sql
SELECT *
FROM movies
WHERE year < 2000
OR year > 2010;
```

---

### Task 4: Find the First 5 Pixar Movies and Their Release Year

```sql
SELECT title, year
FROM movies
ORDER BY year
LIMIT 5;
```

Output:

| title          | year |
| -------------- | ---- |
| Toy Story      | 1995 |
| A Bug's Life   | 1998 |
| Toy Story 2    | 1999 |
| Monsters, Inc. | 2001 |
| Finding Nemo   | 2003 |

---

## 10. Real World Use Cases

### Employees with Salary Greater Than 50000

```sql
SELECT *
FROM Employees
WHERE salary > 50000;
```

---

### Products Between ₹1000 and ₹5000

```sql
SELECT *
FROM Products
WHERE price BETWEEN 1000 AND 5000;
```

---

### Orders from Specific Customers

```sql
SELECT *
FROM Orders
WHERE customer_id IN (101, 102, 103);
```

---

## 11. Common Mistakes

### Mistake 1

Wrong:

```sql
SELECT *
FROM movies
WHERE;
```

Reason:

Condition is missing.

---

### Mistake 2

Wrong:

```sql
SELECT *
FROM movies
WHERE year BETWEEN 2010 AND 2000;
```

Reason:

Lower value should come first.

Correct:

```sql
WHERE year BETWEEN 2000 AND 2010;
```

---

### Mistake 3

Using Multiple OR Conditions Instead of IN

Less Readable:

```sql
WHERE year = 1995
OR year = 1998
OR year = 1999
```

Better:

```sql
WHERE year IN (1995, 1998, 1999)
```

---

## 12. Interview Questions

### Q1. Difference Between BETWEEN and IN?

Answer:

* BETWEEN is used for ranges.
* IN is used for specific values.

Example:

```sql
WHERE year BETWEEN 2000 AND 2010
```

```sql
WHERE year IN (2000, 2005, 2010)
```

---

### Q2. Is BETWEEN Inclusive?

Answer:

Yes.

```sql
WHERE year BETWEEN 2000 AND 2010
```

Includes:

* 2000
* 2010

---

### Q3. Difference Between != and <> ?

Answer:

Both mean "Not Equal To".

```sql
WHERE year != 2000
```

```sql
WHERE year <> 2000
```

Both are valid.

---

### Q4. Which Executes First?

```sql
SELECT *
FROM movies
WHERE year > 2000;
```

Answer:

WHERE executes before SELECT.

---

## 13. Hands-On Practice

### Practice 1

Find movies released after 2005.

```sql
SELECT *
FROM movies
WHERE year > 2005;
```

---

### Practice 2

Find movies released before 2000.

```sql
SELECT *
FROM movies
WHERE year < 2000;
```

---

### Practice 3

Find movies released in 1995, 1998, and 1999.

```sql
SELECT *
FROM movies
WHERE year IN (1995, 1998, 1999);
```

---

### Practice 4

Find movies released outside the range 2000–2010.

```sql
SELECT *
FROM movies
WHERE year NOT BETWEEN 2000 AND 2010;
```

---

## 14. Key Takeaways

* WHERE filters rows.
* SQL executes WHERE before SELECT.
* BETWEEN is used for ranges.
* IN is used for multiple values.
* NOT BETWEEN excludes a range.
* NOT IN excludes specific values.
* WHERE improves query performance.

---

## 15. Revision Notes

```sql
SELECT *
FROM table_name
WHERE condition;
```

### Most Used Patterns

```sql
WHERE column = value
```

```sql
WHERE column > value
```

```sql
WHERE column BETWEEN value1 AND value2
```

```sql
WHERE column NOT BETWEEN value1 AND value2
```

```sql
WHERE column IN (value1, value2)
```

```sql
WHERE column NOT IN (value1, value2)
```

---

## 16. My Learning

Date: __________

Topic: WHERE Clause (Numeric Filtering)

What I Learned:

* WHERE filters rows.
* Comparison operators help filter numeric values.
* BETWEEN works with ranges.
* IN works with multiple values.
* SQL executes WHERE before SELECT.

Difficulty Level: Easy

Confidence: ____ / 10
`\