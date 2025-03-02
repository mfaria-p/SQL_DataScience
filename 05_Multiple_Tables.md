# Working with Multiple Tables in SQL

## Overview

This document summarizes the key concepts and techniques learned about working with multiple tables in SQL. There are several ways to access multiple tables in the same query, including sub-queries, implicit joins, and explicit join operators such as INNER JOIN and OUTER JOIN.

## Techniques for Accessing Multiple Tables

### 1. Using Sub-Queries

Sub-queries allow us to retrieve data from one table based on a condition that depends on another table. This method is useful for filtering results dynamically.

#### Example 1: Filtering Employees Based on Department ID

```sql
SELECT * FROM Employees
WHERE Department_ID IN (SELECT Department_ID FROM Departments);
```

- The outer query retrieves all employee records.
- The sub-query selects department IDs from the Departments table, filtering the employee records accordingly.

#### Example 2: Filtering Employees Based on Location ID

```sql
SELECT * FROM Employees
WHERE DEP_ID IN (SELECT DEP_ID_DEP FROM Departments WHERE LOC_ID = 'L0002');
```

- The sub-query filters departments based on location.
- The outer query retrieves employees belonging to those departments.

#### Example 3: Retrieving Department Information for Employees with Salaries Above \$70,000

```sql
SELECT Department_ID, Department_Name FROM Departments
WHERE Department_ID IN (SELECT Department_ID FROM Employees WHERE Salary > 70000);
```

- The sub-query selects department IDs where employees earn more than \$70,000.
- The outer query retrieves department details for those IDs.

### 2. Using Implicit Joins

Instead of using sub-queries, we can specify multiple tables in the `FROM` clause to perform implicit joins.

#### Example 1: Cartesian Join (Full Join)

```sql
SELECT * FROM Employees, Departments;
```

- Every row in Employees is joined with every row in Departments.
- This results in a large dataset where all possible combinations are included.

#### Example 2: Filtering the Join with a Condition

```sql
SELECT * FROM Employees, Departments
WHERE Employees.DEP_ID = Departments.DEP_ID_DEP;
```

- This ensures that only matching department records are included.

#### Example 3: Using Aliases for Readability

```sql
SELECT E.EMP_ID, D.DEP_NAME FROM Employees E, Departments D
WHERE E.DEP_ID = D.DEP_ID_DEP;
```

- `E` is used as an alias for Employees.
- `D` is used as an alias for Departments.
- This improves readability and maintainability of the query.

## Summary

In this lesson, we explored two methods for working with multiple tables in SQL:

1. **Sub-Queries**: Useful for filtering and retrieving related data from different tables.
2. **Implicit Joins**: Allow combining data from multiple tables by specifying them in the `FROM` clause and using a `WHERE` condition.

Understanding these methods enhances the ability to perform complex queries efficiently. Further learning should include explicit join operators (INNER JOIN, LEFT JOIN, RIGHT JOIN, FULL OUTER JOIN) for more advanced data retrieval techniques.

