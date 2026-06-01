# Filtering and Sorting Query Results (DISTINCT, ORDER BY, LIMIT, OFFSET)

## 1. Definition

When working with large datasets, we often need to:

* Remove duplicate values
* Sort records in a specific order
* Return only a limited number of rows
* Skip a certain number of rows

SQL provides the following clauses for this purpose:

* DISTINCT
* ORDER BY
* LIMIT
* OFFSET

These clauses make query results more organized and efficient.

---

## 2. Why Do We Need Them?

Imagine a Movies table with millions of records.

Without sorting:

```text
Cars
Toy Story
Up
Finding Nemo
```

The results may appear in any order.

We may need:

* Movies sorted alphabetically
* Latest movies first
* Unique directors only
* Top 5 records

This is where DISTINCT, ORDER BY, LIMIT, and OFFSET help.

---

## 3. Syntax

### DISTINCT

```sql
SELECT DISTINCT column_name
FROM table_name;
```

### ORDER BY

```sql
SELECT column_name
FROM table_name
ORDER BY column_name ASC;
```

### ORDER BY Descending

```sql
SELECT column_name
FROM table_name
ORDER BY column_name DESC;
```

### LIMIT

```sql
SELECT *
FROM table_name
LIMIT 5;
```

### LIMIT with OFFSET

```sql
SELECT *
FROM table_name
LIMIT 5 OFFSET 5;
```

---

## 4. SQL Query Execution Order

Example:

```sql
SELECT DISTINCT director
FROM movies
ORDER BY director;
```

Execution Order:

1. FROM
2. SELECT
3. DISTINCT
4. ORDER BY

---

Example:

```sql
SELECT *
FROM movies
ORDER BY year DESC
LIMIT 5;
```

Execution Order:

1. FROM
2. SELECT
3. ORDER BY
4. LIMIT

---

## 5. DISTINCT Keyword

### Purpose

Removes duplicate rows from the result.

### Example

Movies Table

| director      |
| ------------- |
| John Lasseter |
| John Lasseter |
| Brad Bird     |
| Brad Bird     |
| Pete Docter   |

Query:

```sql
SELECT DISTINCT director
FROM movies;
```

Output:

| director      |
| ------------- |
| John Lasseter |
| Brad Bird     |
| Pete Docter   |

Duplicate values are removed.

---

## 6. ORDER BY Clause

### Purpose

Sorts query results.

### Ascending Order (Default)

```sql
SELECT title
FROM movies
ORDER BY title ASC;
```

Output:

```text
A Bug's Life
Brave
Cars
Finding Nemo
...
```

---

### Descending Order

```sql
SELECT title
FROM movies
ORDER BY title DESC;
```

Output:

```text
Up
WALL-E
Toy Story
...
```

---

## 7. Sorting Numeric Data

### Oldest Movies First

```sql
SELECT title, year
FROM movies
ORDER BY year ASC;
```

---

### Latest Movies First

```sql
SELECT title, year
FROM movies
ORDER BY year DESC;
```

---

## 8. LIMIT Clause

### Purpose

Returns only a specified number of rows.

Example:

```sql
SELECT *
FROM movies
LIMIT 5;
```

Returns only the first 5 rows.

---

## 9. OFFSET Clause

### Purpose

Skips a specific number of rows.

Example:

```sql
SELECT *
FROM movies
LIMIT 5 OFFSET 5;
```

Meaning:

```text
Skip first 5 rows
Return next 5 rows
```

---

## 10. Combining ORDER BY and LIMIT

### Latest 3 Movies

```sql
SELECT title, year
FROM movies
ORDER BY year DESC
LIMIT 3;
```

Output:

```text
Monsters University
Brave
Cars 2
```

---

## 11. Sample Data

| title               | year |
| ------------------- | ---- |
| Toy Story           | 1995 |
| A Bug's Life        | 1998 |
| Toy Story 2         | 1999 |
| Monsters, Inc.      | 2001 |
| Finding Nemo        | 2003 |
| Cars                | 2006 |
| Ratatouille         | 2007 |
| WALL-E              | 2008 |
| Up                  | 2009 |
| Toy Story 3         | 2010 |
| Cars 2              | 2011 |
| Brave               | 2012 |
| Monsters University | 2013 |

---

## 12. SQLBolt Exercise Solutions

### Task 1: List All Directors Alphabetically Without Duplicates

```sql
SELECT DISTINCT director
FROM movies
ORDER BY director ASC;
```

---

### Task 2: List Last Four Pixar Movies Released

```sql
SELECT title, year
FROM movies
ORDER BY year DESC
LIMIT 4;
```

Output:

```text
Monsters University
Brave
Cars 2
Toy Story 3
```

---

### Task 3: List First Five Pixar Movies Sorted Alphabetically

```sql
SELECT title
FROM movies
ORDER BY title ASC
LIMIT 5;
```

Output:

```text
A Bug's Life
Brave
Cars
Cars 2
Finding Nemo
```

---

### Task 4: List Next Five Pixar Movies Sorted Alphabetically

```sql
SELECT title
FROM movies
ORDER BY title ASC
LIMIT 5 OFFSET 5;
```

Output:

```text
Monsters, Inc.
Monsters University
Ratatouille
The Incredibles
Toy Story
```

---

## 13. Real World Use Cases

### Top 10 Highest Paid Employees

```sql
SELECT *
FROM Employees
ORDER BY salary DESC
LIMIT 10;
```

---

### Latest 5 Orders

```sql
SELECT *
FROM Orders
ORDER BY order_date DESC
LIMIT 5;
```

---

### Unique Cities

```sql
SELECT DISTINCT city
FROM Customers;
```

---

### Pagination

Page 1:

```sql
SELECT *
FROM Products
LIMIT 10 OFFSET 0;
```

Page 2:

```sql
SELECT *
FROM Products
LIMIT 10 OFFSET 10;
```

Page 3:

```sql
SELECT *
FROM Products
LIMIT 10 OFFSET 20;
```

---

## 14. Common Mistakes

### Mistake 1

Wrong:

```sql
SELECT DISTINCT *
FROM movies;
```

Reason:

May not remove duplicates if rows differ in other columns.

Better:

```sql
SELECT DISTINCT director
FROM movies;
```

---

### Mistake 2

Forgetting DESC

Wrong:

```sql
SELECT *
FROM movies
ORDER BY year;
```

Returns oldest first.

Correct:

```sql
SELECT *
FROM movies
ORDER BY year DESC;
```

Returns newest first.

---

### Mistake 3

Using LIMIT Without ORDER BY

Wrong:

```sql
SELECT *
FROM movies
LIMIT 5;
```

Result may be unpredictable.

Better:

```sql
SELECT *
FROM movies
ORDER BY year DESC
LIMIT 5;
```

---

## 15. Interview Questions

### Q1. Difference Between DISTINCT and GROUP BY?

Answer:

DISTINCT removes duplicate values.

```sql
SELECT DISTINCT director
FROM movies;
```

GROUP BY groups rows for aggregation.

```sql
SELECT director, COUNT(*)
FROM movies
GROUP BY director;
```

---

### Q2. What Is the Default Sort Order?

Answer:

Ascending.

```sql
SELECT *
FROM movies
ORDER BY year;
```

Equivalent to:

```sql
SELECT *
FROM movies
ORDER BY year ASC;
```

---

### Q3. Which Executes First?

```sql
SELECT *
FROM movies
ORDER BY year DESC
LIMIT 5;
```

Answer:

1. ORDER BY
2. LIMIT

---

### Q4. Difference Between LIMIT and OFFSET?

Answer:

LIMIT controls how many rows to return.

OFFSET controls how many rows to skip.

Example:

```sql
LIMIT 5 OFFSET 10
```

Means:

```text
Skip first 10 rows
Return next 5 rows
```

---

## 16. Hands-On Practice

### Practice 1

Find all movie titles alphabetically.

```sql
SELECT title
FROM movies
ORDER BY title;
```

---

### Practice 2

Find newest movie.

```sql
SELECT *
FROM movies
ORDER BY year DESC
LIMIT 1;
```

---

### Practice 3

Find unique directors.

```sql
SELECT DISTINCT director
FROM movies;
```

---

### Practice 4

Find oldest three movies.

```sql
SELECT *
FROM movies
ORDER BY year ASC
LIMIT 3;
```

---

### Practice 5

Display movies 6–10 alphabetically.

```sql
SELECT title
FROM movies
ORDER BY title
LIMIT 5 OFFSET 5;
```

---

## 17. Key Takeaways

* DISTINCT removes duplicate values.
* ORDER BY sorts rows.
* ASC means ascending order.
* DESC means descending order.
* LIMIT restricts the number of rows returned.
* OFFSET skips rows before returning results.
* ORDER BY + LIMIT is frequently used in interviews and real applications.

---

## 18. Revision Notes

```sql
SELECT DISTINCT column_name
FROM table_name;
```

```sql
SELECT *
FROM table_name
ORDER BY column_name ASC;
```

```sql
SELECT *
FROM table_name
ORDER BY column_name DESC;
```

```sql
SELECT *
FROM table_name
LIMIT 5;
```

```sql
SELECT *
FROM table_name
LIMIT 5 OFFSET 5;
```

```sql
SELECT *
FROM table_name
ORDER BY column_name DESC
LIMIT 10;
```

---

## 19. My Learning

Date: __________

Topic: DISTINCT, ORDER BY, LIMIT, OFFSET

What I Learned:

* DISTINCT removes duplicate values.
* ORDER BY sorts query results.
* ASC sorts ascending.
* DESC sorts descending.
* LIMIT restricts rows returned.
* OFFSET skips rows.
* These clauses are heavily used for reporting and pagination.

Difficulty Level: Easy

Confidence: ____ / 10
