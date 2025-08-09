# MySQL Tutorial

## Beginner Series

## SELECT Statements
- You can do calculations (e.g., `age + 10`), and it follows **PEMDAS**.
- `SELECT DISTINCT column_name FROM table_name` — brings only the unique values.
- `SELECT DISTINCT first_name, gender FROM employee_demographics;` — all results are unique, checks the two columns as one.

---

## WHERE Statements
- Add conditions using comparison operators:
  - `=`, `!=`, `>`, `<`, `<=`, `>=`, etc.
- **Logical Operators** in the WHERE clause:
  - `AND` — both conditions must be met.
  - `OR` — either of the conditions must be met.
  - `NOT` — negates a condition.
- **PEMDAS** applies to logical operators as well.

---

## LIKE Statements
- Used to look for specific patterns with special characters:
  - `%` — matches any sequence of characters.
  - `_` — matches a single specific character.

---

## GROUP BY
- What you are selecting must either:
  - Match the `GROUP BY` item, **or**
  - Use an aggregate function.

---

## Aggregate Functions
- Common examples:
  - `MAX()` — maximum value
  - `MIN()` — minimum value
  - `AVG()` — average value
  - `COUNT()` — counts rows
- These are often used with `GROUP BY`.

---

## ORDER BY
- Sorts the results in ascending (`ASC`) or descending (`DESC`) order.
- You can use column names or column positions (not best practice).

---

## HAVING vs WHERE
- `HAVING` comes **right after** `GROUP BY`.
- Use `HAVING` instead of `WHERE` to filter using aggregate functions.

---

## LIMIT
- Specifies how many rows you want in your output.
- Can be combined with `ORDER BY` for more powerful queries.
- Example:
  ```sql
  SELECT * 
  FROM employee_demographics 
  ORDER BY age DESC 
  LIMIT 2, 1;

- This means: skip the first 2 rows, then select the 1 that comes next.

---

## Aliasing
- A way to change the name of the column or table.
- Common in joins or when renaming output columns.
- Use the AS keyword (optional, can be omitted).

## Additional Notes
- Always be mindful of **query performance** — using indexes, limiting results, and avoiding unnecessary calculations can help.
- SQL is **case-insensitive** for keywords, but **case-sensitive** for string matching unless configured otherwise.
- Comments in SQL:
Single-line: `-- comment`

Multi-line: `/* comment */`


# Intermediate SQL Notes

## 1. Aliases
- **Definition**: Aliases are temporary names given to a table or column for easier reference.
- **Syntax**:  
  ```sql
  SELECT column_name AS alias_name
  FROM table_name;
  ```
- **Notes**:
  - The `AS` keyword is optional, but using it improves readability.
  - Useful for making query results more readable.

---

## 2. Joins
### Inner Join
- Returns records that have matching values in both tables.
- **Syntax**:
  ```sql
  SELECT columns
  FROM table1
  INNER JOIN table2
  ON table1.column = table2.column;
  ```

### Left Join (Left Outer Join)
- Returns all records from the left table and matching records from the right table.
- **Syntax**:
  ```sql
  SELECT columns
  FROM table1
  LEFT JOIN table2
  ON table1.column = table2.column;
  ```

### Right Join (Right Outer Join)
- Returns all records from the right table and matching records from the left table.
- **Syntax**:
  ```sql
  SELECT columns
  FROM table1
  RIGHT JOIN table2
  ON table1.column = table2.column;
  ```

### Full Outer Join
- Returns all records from both tables, with NULLs where there is no match.
- **Note**: Not all SQL databases support `FULL JOIN` directly (e.g., MySQL doesn’t).

---

## 3. UNION and UNION ALL
- **UNION**: Combines results from multiple queries, removing duplicates.
- **UNION ALL**: Combines results from multiple queries, keeping duplicates.
- **Syntax**:
  ```sql
  SELECT column_name FROM table1
  UNION
  SELECT column_name FROM table2;
  ```

---

## 4. Subqueries
- A query inside another query.
- Can be used in:
  - `SELECT`
  - `FROM`
  - `WHERE`
- **Example**:
  ```sql
  SELECT *
  FROM employees
  WHERE salary > (SELECT AVG(salary) FROM employees);
  ```

---

## 5. GROUP BY and HAVING
- **GROUP BY**: Groups rows that have the same values into summary rows.
- **HAVING**: Filters groups (similar to `WHERE` but for grouped results).
- **Example**:
  ```sql
  SELECT department, COUNT(*) AS employee_count
  FROM employees
  GROUP BY department
  HAVING COUNT(*) > 5;
  ```

---

## 6. CASE Statements
- Allows conditional logic in SQL.
- **Syntax**:
  ```sql
  SELECT name,
         CASE
             WHEN score >= 90 THEN 'A'
             WHEN score >= 75 THEN 'B'
             ELSE 'C'
         END AS grade
  FROM students;
  ```

---

## 7. Indexes
- **Purpose**: Improve the speed of data retrieval.
- **Syntax**:
  ```sql
  CREATE INDEX index_name
  ON table_name (column_name);
  ```
- **Notes**:
  - Improves read performance.
  - Can slow down insert/update/delete operations.
  - Use on columns that are frequently searched or used in joins.

---

## 8. Constraints
- **Types**:
  - `NOT NULL` – Ensures a column cannot have a NULL value.
  - `UNIQUE` – Ensures all values in a column are different.
  - `PRIMARY KEY` – Uniquely identifies each row.
  - `FOREIGN KEY` – Links rows between tables.
  - `CHECK` – Ensures values meet a specific condition.
  - `DEFAULT` – Sets a default value when no value is provided.

---

## 9. Transactions
- **Purpose**: Group SQL statements into a single unit of work.
- **Commands**:
  - `START TRANSACTION` / `BEGIN`
  - `COMMIT` – Saves changes.
  - `ROLLBACK` – Reverts changes.
- **Example**:
  ```sql
  START TRANSACTION;
  UPDATE accounts SET balance = balance - 100 WHERE id = 1;
  UPDATE accounts SET balance = balance + 100 WHERE id = 2;
  COMMIT;
  ```

---

## 10. Views
- **Definition**: A stored query that can be treated like a table.
- **Syntax**:
  ```sql
  CREATE VIEW view_name AS
  SELECT columns
  FROM table
  WHERE condition;
  ```
- **Notes**:
  - Simplifies complex queries.
  - Can be used to restrict data access.
