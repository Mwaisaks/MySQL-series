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
