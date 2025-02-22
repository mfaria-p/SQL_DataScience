# What I Learned About SQL and Databases

## 1⃣ Introduction to SQL  
- **SQL (Structured Query Language)** is used to query and manage relational databases.  
- **Data** is a collection of facts (words, numbers, pictures) and is essential in various industries.  
- **Databases** store and organize data securely for quick access.  
- **Relational Databases** store data in tables with columns and rows, allowing relationships between tables.  
- **RDBMS (Relational Database Management System)** is software that manages relational databases (e.g., MySQL, Oracle, DB2).  

---

## 2⃣ Retrieving Data with `SELECT`  
### Basic `SELECT` Statement  
The `SELECT` statement is a **Database Query command** used to retrieve information from a table.  

#### Syntax:
```sql
SELECT COLUMN1, COLUMN2 FROM TABLE_1;
```
To retrieve all columns from a table:
```sql
SELECT * FROM TABLE_1;
```

### Using `WHERE` Clause for Filtering  
The `WHERE` clause filters the data based on a predicate (condition).  

#### Syntax:
```sql
SELECT COLUMN1, COLUMN2 FROM TABLE_1 WHERE <predicate>;
```
#### Example:
Retrieve the title of the book with `book_id = 'B1'`:
```sql
SELECT book_id, title FROM book WHERE book_id = 'B1';
```

### Comparison Operators in SQL  
- `=` → Equal to  
- `>` → Greater than  
- `<` → Less than  
- `>=` → Greater than or equal to  
- `<=` → Less than or equal to  
- `<>` or `!=` → Not equal to  

🔹 **SQL keywords (`SELECT`, `FROM`, `WHERE`, etc.) are case insensitive**, but they are often written in **all caps** for readability.  
🔹 **Table and column names may be case-sensitive depending on the database system.**  

---

## 3⃣ Useful Expressions in `SELECT` Statements  
### COUNT – Retrieves the number of rows that match a condition.  
```sql
SELECT COUNT(*) FROM tablename;
```
```sql
SELECT COUNT(COUNTRY) FROM MEDALS WHERE COUNTRY = 'CANADA';
```

### DISTINCT – Removes duplicate values from a result set.  
```sql
SELECT DISTINCT columnname FROM tablename;
```

### LIMIT – Restricts the number of rows retrieved.  
```sql
SELECT * FROM tablename LIMIT 10;
```

### OFFSET – Skips a specific number of rows before retrieving results.  
```sql
SELECT * FROM MEDALS LIMIT 5 OFFSET 10;
```
🔹 **Important:** `OFFSET` **must** be written **after** `LIMIT`.  

---

## 4⃣ Inserting and Modifying Data  

### INSERT INTO – Adding Data to a Table  
```sql
INSERT INTO tablename (column1, column2, column3)
VALUES (value1, value2, value3);
```

### UPDATE – Modifying Existing Data  
```sql
UPDATE tablename
SET column1 = value1, column2 = value2
WHERE condition;
```

### DELETE – Removing Data from a Table  
```sql
DELETE FROM tablename WHERE condition;
```
#### ⚠️ **Important:** If you run a `DELETE FROM` statement on a table **without a `WHERE` clause**, **all rows in the table will be deleted**. However, the **table structure and its columns remain intact**.

---

## 5⃣ SQL Keyword Order Matters  
SQL statements must follow a specific order:  
```sql
SELECT column1, column2
FROM tablename
WHERE condition
GROUP BY column
HAVING condition
ORDER BY column
LIMIT number OFFSET number;
```

---

## 6⃣ Using Quotes in SQL (`'` vs. `"`)  

### Single Quotes (`'`) – For String Literals  
- **Use single quotes for text (string) values in queries.**  
- **Example:**  
  ```sql
  SELECT * FROM FilmLocations WHERE Location = 'City Hall';
  ```
- **Wrong Usage:**  
  ```sql
  SELECT * FROM FilmLocations WHERE Location = "City Hall"; -- ❌ Might cause errors
  ```
🔹 **Key Rule:** Always use single quotes (`'`) around string values.

### Double Quotes (`"`) – For Identifiers (Column and Table Names)  
- **Use double quotes if the column or table name:**  
  - Contains spaces or special characters.  
  - Is case-sensitive.  
  - Matches an SQL reserved keyword.  

- **Example:**  
  ```sql
  SELECT "First Name", "Last Name" FROM "User Data";
  ```
- **Example (reserved keyword as column name):**  
  ```sql
  SELECT "Order", "Date" FROM Sales;
  ```

---

## 7⃣ Installing and Running Datasette  
Datasette is a tool for exploring and publishing data.  

### Installation:  
```sh
pip install datasette
```

### Running Datasette:  
```sh
datasette
```

### Accessing a Database in Datasette  
To open a specific SQLite database:  
```sh
datasette my_database.db
```
Access it in your browser at:  
```
http://127.0.0.1:8001
```
🔹 Click on the database name to view available tables.  
🔹 Click on a table to browse its data.  
🔹 You can run SQL queries directly from the Datasette interface.  

---

This knowledge helps in understanding how data is stored, managed, retrieved, and accessed efficiently using SQL and Datasette. 🚀  

