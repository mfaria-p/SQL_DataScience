# Introduction to Relational Databases and DDL Statements

## Overview

Relational databases are the most widely used data model for databases because they provide data independence and a simple data structure. In this document, i give an overview of the different types of models, the mapping of data to tables, and how relationships between tables are defined.

## The Relational Model

The relational model stores data in a structured format using tables, which provides:

- **Logical Data Independence**: The structure of the database can change without affecting applications that access the data.
- **Physical Data Independence**: The storage structure of the database can be altered without changing its logical structure.
- **Storage Independence**: Data is stored separately from applications, ensuring flexibility.

### Entity-Relationship (ER) Model

The ER model is an alternative to the relational model and is often used to design relational databases. It represents data as a collection of **entities** and their **relationships**.

#### Example: Library Database

- **Entities (Tables)**:
  - **Book**: Represents books in the library.
  - **Author**: Represents authors of books.
  - **Borrower**: Represents library members.
  - **Loan**: Represents book borrowings.
  - **Copy**: Represents copies of books available.
- **Relationships**:
  - A book can be written by one or multiple authors.
  - A library can have multiple copies of a book.
  - A borrower can borrow only one copy of a book at a time.

### Mapping Entities to Tables

- **Entities** become **tables** in the relational database.
- **Attributes** of entities become **columns** in tables.
- **Rows (Tuples)** in a table represent individual data records.
- Example: The `Book` entity has attributes such as:
  - `Title` (VARCHAR)
  - `Edition` (INTEGER)
  - `Year` (INTEGER)
  - `ISBN` (CHAR)

### Data Types

- **CHAR vs. VARCHAR**:

  - `CHAR(n)`: Stores fixed-length strings of `n` characters, padding shorter values with spaces.
  - `VARCHAR(n)`: Stores variable-length strings up to `n` characters, using only the necessary storage space.
  - Use `CHAR` when all values have the same length (e.g., country codes), and `VARCHAR` when lengths vary (e.g., names).

- **Character Data**: Use `CHAR` for fixed-length strings and `VARCHAR` for variable-length strings.

- **Numeric Data**: Includes types such as `INTEGER` and `DECIMAL`.

- **Timestamps**: Include `DATE`, `TIME`, and `DATETIME` types.

### Primary and Foreign Keys

- **Primary Key**: Uniquely identifies each row in a table (e.g., `ISBN` in the `Book` table).
- **Foreign Key**: A column that references a primary key in another table to create relationships (e.g., `Author_ID` in the `Book` table referencing `Author_ID` in the `Author` table).

## SQL Statements for Relational Databases

SQL (Structured Query Language) is used to interact with tables, columns, and rows in relational databases. SQL statements are categorized into:

### Data Definition Language (DDL)

Used to define or modify database structures:

- `CREATE` – Create tables and define columns.
- `ALTER` – Modify existing tables (add/drop columns, change data types).
- `TRUNCATE` – Delete all data from a table but retain its structure.
- `DROP` – Delete an entire table.

#### The CREATE Statement

The `CREATE` statement is used to create tables and define their structure. The syntax is as follows:

```sql
CREATE TABLE table_name (
    column_name1 DATA_TYPE constraints,
    column_name2 DATA_TYPE constraints,
    ...
);
```

Example: Creating tables for a pet sales database:

```sql
CREATE TABLE PETSALE (
    ID INTEGER NOT NULL,
    PET CHAR(20),
    SALEPRICE DECIMAL(6,2),
    PROFIT DECIMAL(6,2),
    SALEDATE DATE
);

CREATE TABLE PET (
    ID INTEGER NOT NULL,
    ANIMAL VARCHAR(20),
    QUANTITY INTEGER
);
```

#### The ALTER Statement

The `ALTER TABLE` statement modifies an existing table structure. It can be used to add or remove columns, change data types, rename columns, or modify constraints.

To add a column:

```sql
ALTER TABLE PETSALE ADD COLUMN QUANTITY INTEGER;
```

To update values in the newly added column:

```sql
UPDATE PETSALE SET QUANTITY = 9 WHERE ID = 1;
UPDATE PETSALE SET QUANTITY = 3 WHERE ID = 2;
UPDATE PETSALE SET QUANTITY = 2 WHERE ID = 3;
UPDATE PETSALE SET QUANTITY = 6 WHERE ID = 4;
UPDATE PETSALE SET QUANTITY = 24 WHERE ID = 5;
SELECT * FROM PETSALE;
```

To modify a column's data type:

```sql
ALTER TABLE PETSALE MODIFY PET VARCHAR(20);
```

To rename a column:

```sql
ALTER TABLE PETSALE CHANGE PET ANIMAL VARCHAR(20);
```

To remove a column:

```sql
ALTER TABLE PETSALE DROP COLUMN PROFIT;
```

#### The DROP Statement

The `DROP TABLE` statement removes an entire table from the database, including all its data.

```sql
DROP TABLE author;
```

#### The TRUNCATE Statement

The `TRUNCATE TABLE` statement removes all rows from a table but retains the table structure.

```sql
TRUNCATE TABLE author IMMEDIATE;
```

### Data Manipulation Language (DML)

Used to manipulate data within tables:

- `INSERT` – Add new rows.
- `SELECT` – Retrieve data from tables.
- `UPDATE` – Modify existing data.
- `DELETE` – Remove data from tables.

## Conclusion

Relational databases offer structured data storage with logical and physical independence. By using entity-relationship modeling, we can design efficient databases, map entities to tables, and enforce data integrity through primary and foreign keys. SQL provides powerful tools for defining, querying, and manipulating data efficiently.

