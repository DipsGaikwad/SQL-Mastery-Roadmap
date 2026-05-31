# Text Filtering with LIKE, IN, and Wildcards

## 1. Definition

When working with text data in SQL, the WHERE clause supports special operators that help us:

* Search for specific text values
* Match patterns in strings
* Search using wildcards
* Check multiple values at once
;;lh
These operators are commonly used in search features, reports, and filtering textual data.

---

## 2. Why Do We Need Text Filtering?

Suppose we have thousands of movie records.

Instead of finding exact matches manually, SQL allows us to:

* Find all movies starting with "Toy"
* Find all directors named "John Lasseter"
* Find all movies containing the word "Story"
* Find records matching multiple values

---

## 3. Syntax

### Exact Match

```sql
SELECT *
FROM table_name
WHERE column_name = 'value';
```

### Pattern Matching

```sql
SELECT *
FROM table_name
WHERE column_name LIKE 'pattern';
```

### Multiple Values

```sql
SELECT *
FROM table_name
WHERE column_name IN ('value1', 'value2');
```

---

## 4. Operators Overview

| Operator | Description                     |
| -------- | ------------------------------- |
| =        | Exact match                     |
| != or <> | Not equal                       |
| LIKE     | Pattern matching                |
| NOT LIKE | Opposite of LIKE                |
| %        | Matches zero or more characters |
| _        | Matches exactly one character   |
| IN()     | Matches any value in a list     |
| NOT IN() | Excludes values in a list       |

---

## 5. Sample Data

### Movies Table

| id | title        | director       |
| -- | ------------ | -------------- |
| 1  | Toy Story    | John Lasseter  |
| 2  | A Bug's Life | John Lasseter  |
| 3  | Toy Story 2  | John Lasseter  |
| 9  | WALL-E       | Andrew Stanton |
| 87 | WALL-G       | Brenda Chapman |

---

## 6. Exact Match Using =

### Find Movies Directed by John Lasseter

```sql
SELECT *
FROM movies
WHERE director = 'John Lasseter';
```

Output:

* Toy Story
* A Bug's Life
* Toy Story 2h
* Cars
* Cars 2

---

## 7. Not Equal Operator

### Using !=

```sql
SELECT *
FROM movies
WHERE director != 'John Lasseter';
```

### Using <>

```sql
SELECT *
FROM movies
WHERE director <> 'John Lasseter';
```

Both queries produce the same result.

---

## 8. LIKE Operator

The LIKE operator is used for pattern matching.

### Find All Toy Story Movies

```sql
SELECT *
FROM movies
WHERE title LIKE 'Toy Story%';
```

Output:

* Toy Story
* Toy Story 2
* Toy Story 3

---

## 9. Wildcard: %

The percent symbol (%) represents:

"Zero or more characters"

### Example 1

```sql
SELECT *
FROM movies
WHERE title LIKE 'Toy%';
```

Matches:

```text
Toy Story
Toy Story 2
Toy Story 3
```

---

### Example 2

```sql
SELECT *
FROM movies
WHERE title LIKE '%Story%';
```

Matches:

```text
Toy Story
Toy Story 2
Toy Story 3
```

Because "Story" appears anywhere in the title.

---

### Example 3

```sql
SELECT *
FROM movies
WHERE title LIKE '%University';
```

Matches:

```text
Monsters University
```

---

## 10. Wildcard: _

The underscore (_) represents:

"Exactly one character"

### Example

```sql
SELECT *
FROM movies
WHERE title LIKE 'WALL-_';
```

Matches:

```text
WALL-E
WALL-G
```

Does not match:

```text
WALL-EE
```

because `_` can match only one character.

---

## 11. NOT LIKE

Used to exclude patterns.

### Example

```sql
SELECT *
FROM movies
WHERE title NOT LIKE 'Toy%';
```

Returns all movies except Toy Story movies.

---

## 12. IN Operator

Used when checking multiple values.

### Example

```sql
SELECT *
FROM movies
WHERE director IN ('John Lasseter', 'Brad Bird');
```

Equivalent to:

```sql
SELECT *
FROM movies
WHERE director = 'John Lasseter'
OR director = 'Brad Bird';
```

---

## 13. NOT IN Operator

### Example

```sql
SELECT *
FROM movies
WHERE director NOT IN ('John Lasseter', 'Brad Bird');
```

Returns movies directed by everyone except those directors.

---

## 14. SQL Query Execution Order

Example:

```sql
SELECT title
FROM movies
WHERE title LIKE 'Toy%';
```

Execution Order:

1. FROM
2. WHERE
3. SELECT

Step 1:

Read rows from movies table.

Step 2:

Filter rows matching "Toy%".

Step 3:

Return title column.

---

## 15. SQLBolt Exercise Solutions

### Task 1: Find All Toy Story Movies

```sql
SELECT *
FROM movies
WHERE title LIKE 'Toy Story%';
```

---

### Task 2: Find All Movies Directed by John Lasseter

```sql
SELECT *
FROM movies
WHERE director = 'John Lasseter';
```

---

### Task 3: Find All Movies (and Director) Not Directed by John Lasseter

```sql
SELECT title, director
FROM movies
WHERE director != 'John Lasseter';
```

---

### Task 4: Find All WALL-* Movies

```sql
SELECT *
FROM movies
WHERE title LIKE 'WALL-%';
```

---

## 16. Real World Use Cases

### Search Products Starting with iPhone

```sql
SELECT *
FROM Products
WHERE product_name LIKE 'iPhone%';
```

---

### Search Employees by Name

```sql
SELECT *
FROM Employees
WHERE employee_name LIKE 'A%';
```

---

### Find Customers from Multiple Cities

```sql
SELECT *
FROM Customers
WHERE city IN ('Pune', 'Mumbai', 'Delhi');
```

---

## 17. Common Mistakes

### Mistake 1

Wrong:

```sql
SELECT *
FROM movies
WHERE director = John Lasseter;
```

Reason:

Strings must be enclosed in quotes.

Correct:

```sql
SELECT *
FROM movies
WHERE director = 'John Lasseter';
```

---

### Mistake 2

Confusing % and _

```sql
LIKE 'A%'
```

Matches:

```text
A
AB
ABC
APPLE
```

---

```sql
LIKE 'A_'
```

Matches:

```text
AB
AX
A1
```

Only one character after A.

---

### Mistake 3

Using IN Without Parentheses

Wrong:

```sql
WHERE city IN 'Pune','Mumbai'
```

Correct:

```sql
WHERE city IN ('Pune','Mumbai')
```

---

## 18. Interview Questions

### Q1. Difference Between % and _?

Answer:

* % matches zero or more characters.
* _ matches exactly one character.

---

### Q2. Difference Between IN and OR?

Answer:

```sql
WHERE city IN ('Pune','Mumbai')
```

is equivalent to

```sql
WHERE city='Pune'
OR city='Mumbai'
```

IN is cleaner and easier to read.

---

### Q3. Why Must Strings Be Enclosed in Quotes?

Answer:

SQL distinguishes string values from column names and keywords using quotes.

---

### Q4. Difference Between LIKE and = ?

Answer:

```sql
WHERE title = 'Toy Story'
```

Exact match only.

```sql
WHERE title LIKE 'Toy%'
```

Pattern matching.

---

## 19. Hands-On Practice

### Practice 1

Find all movies starting with "Cars".

```sql
SELECT *
FROM movies
WHERE title LIKE 'Cars%';
```

---

### Practice 2

Find all movies containing "Story".

```sql
SELECT *
FROM movies
WHERE title LIKE '%Story%';
```

---

### Practice 3

Find movies directed by Pete Docter or Brad Bird.

```sql
SELECT *
FROM movies
WHERE director IN ('Pete Docter', 'Brad Bird');
```

---

### Practice 4

Find movies not directed by Andrew Stanton.

```sql
SELECT *
FROM movies
WHERE director != 'Andrew Stanton';
```

---

## 20. Key Takeaways

* LIKE is used for pattern matching.
* % matches multiple characters.
* _ matches exactly one character.
* IN checks multiple values.
* NOT IN excludes multiple values.
* Strings must be enclosed in quotes.
* LIKE is one of the most frequently asked SQL interview topics.

---

## 21. Revision Notes

```sql
WHERE column = 'value'
```

```sql
WHERE column != 'value'
```

```sql
WHERE column LIKE 'A%'
```

```sql
WHERE column LIKE '%A%'
```

```sql
WHERE column LIKE 'A_'
```

```sql
WHERE column IN ('A','B','C')
```

```sql
WHERE column NOT IN ('A','B','C')
```

---

## 22. My Learning

Date: __________

Topic: Text Filtering with LIKE and IN

What I Learned:

* LIKE performs pattern matching.
* % matches multiple characters.
* _ matches one character.
* IN checks multiple values.
* Strings require quotes.
* Text filtering is heavily used in real applications.

Difficulty Level: Easy

Confidence: ____ / 10
