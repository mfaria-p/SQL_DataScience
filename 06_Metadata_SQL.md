# Getting Information About Tables and Columns in SQLite and MySQL

## Introduction
This document provides instructions on how to retrieve a list of tables and their column attributes in SQLite and MySQL databases. These commands help users explore the structure of a database, especially when they are unsure of table names or column properties.

## Retrieving a List of Tables
### SQLite
In SQLite, the `sqlite_master` table stores metadata about tables. You can use the following SQL query to list all tables in an SQLite database:
```sql
SELECT name FROM sqlite_master WHERE type='table';
```

### MySQL
In MySQL, you can retrieve the list of tables using the `SHOW TABLES` command:
```sql
SHOW TABLES;
```

## Retrieving Column Information
### SQLite
To get the column names and attributes of a table in SQLite, use the `PRAGMA table_info` command:
```sql
SELECT * FROM PRAGMA table_info(table_name);
```
Replace `table_name` with the actual name of the table you want to inspect.

To count the number of columns in an SQLite table, use:
```sql
SELECT COUNT(*) FROM PRAGMA_table_info('table_name');
```
Replace `table_name` with the actual table name.

### MySQL
To retrieve column details of a table in MySQL, use the `DESCRIBE` statement:
```sql
DESCRIBE table_name;
```
Or alternatively, use:
```sql
SHOW COLUMNS FROM table_name;
```
Replace `table_name` with the name of the table you want to inspect.

## Summary
- To list tables in **SQLite**: `SELECT name FROM sqlite_master WHERE type='table';`
- To list tables in **MySQL**: `SHOW TABLES;`
- To get column details in **SQLite**: `PRAGMA table_info(table_name);`
- To count columns in **SQLite**: `SELECT COUNT(*) FROM PRAGMA_table_info('table_name');`
- To get column details in **MySQL**: `DESCRIBE table_name;` or `SHOW COLUMNS FROM table_name;`

These commands help in understanding the structure of a database efficiently.

