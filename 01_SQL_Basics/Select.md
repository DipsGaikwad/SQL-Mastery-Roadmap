# SELECT Statement

## 1. Definition

The `SELECT` statement is used to retrieve data from one or more columns of a table.

It is the most frequently used SQL command and forms the foundation of almost every SQL query.

---

## 2. Syntax

### Select Specific Columns

```sql
SELECT column_name1, column_name2
FROM table_name;
```

### Select All Columns

```sql
SELECT *
FROM table_name;
```

---

## 3. Example

### Movies Table

| id | title        | director      | year |
| -- | ------------ | ------------- | ---- |
| 1  | Toy Story    | John Lasseter | 1995 |
| 2  | A Bug's Life | John Lasseter | 1998 |

### Retrieve Movie Titles

```sql
SELECT title
FROM movies;
```

Output:

| title        |
| ------------ |
| Toy Story    |
| A Bug's Life |

---

### Retrieve Title and Director

```sql
SELECT title, director
FROM movies;
```

Output:

| title        | director      |
| ------------ | ------------- |
| Toy Story    | John Lasseter |
| A Bug's Life | John Lasseter |

---

### Retrieve All Columns

```sql
SELECT *
FROM movies;
```

Output:

Returns every column and every row from the table.

---

## 4. Real World Use Cases

1. Display customer names.
2. Show employee details.
3. Generate sales reports.
4. Retrieve product information.
5. Create dashboard reports.

Example:

```sql
SELECT customer_name, city
FROM Customers;
```

---

## 5. Common Mistakes

### Mistake 1

Wrong:

```sql
SELECT FROM movies;
```

Reason:

Column names are missing.

Correct:

```sql
SELECT title
FROM movies;
```

---

### Mistake 2

Using `SELECT *` unnecessarily.

Wrong:

```sql
SELECT *
FROM Employees;
```

When only employee names are required.

Better:

```sql
SELECT employee_name
FROM Employees;
```

Reason:

Retrieving only required columns improves readability and performance.

---

## 6. Interview Questions

### Q1. Difference between:

```sql
SELECT *
```

and

```sql
SELECT column1, column2
```

Answer:

`SELECT *` returns all columns.
Selecting specific columns returns only required data and is generally preferred.

---

### Q2. Why should we avoid `SELECT *` in production?

Answer:

* Retrieves unnecessary data.
* Reduces performance.
* Makes code harder to maintain.

---

## 7. SQLBolt Practice Queries

### Find title of each film

```sql
SELECT title
FROM movies;
```

### Find director of each film

```sql
SELECT director
FROM movies;
```

### Find title and director

```sql
SELECT title, director
FROM movies;
```

### Find title and year

```sql
SELECT title, year
FROM movies;
```

### Find all information

```sql
SELECT *
FROM movies;
```

---

## 8. Key Takeaways

* SELECT is used to retrieve data.
* Use commas to retrieve multiple columns.
* Use `*` to retrieve all columns.
* Prefer selecting only required columns.
* SELECT is the foundation of SQL querying.

---

## 9. Revision Notes

```sql
SELECT column_name
FROM table_name;
```

```sql
SELECT column1, column2
FROM table_name;
```

```sql
SELECT *
FROM table_name;
```
