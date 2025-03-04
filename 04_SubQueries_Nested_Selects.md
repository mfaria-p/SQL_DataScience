# Subqueries and Nested Selects

## Introduction

Subqueries, also known as sub-selects, are queries nested inside another query, enclosed within parentheses. They enable more complex and powerful queries than would otherwise be possible.

## Example Use Cases

### 1. Subqueries in the WHERE Clause

A common use of subqueries is within the `WHERE` clause to filter records dynamically. Consider the `employees` table, which contains multiple columns such as `employee_id`, `first_name`, `last_name`, `salary`, etc.

#### Problem:

Retrieve a list of employees who earn more than the average salary.

#### Incorrect Attempt:

```sql
SELECT * FROM employees WHERE salary > AVG(salary);
```

This results in an error because aggregate functions like `AVG()` cannot be used directly in the `WHERE` clause.

#### Correct Approach Using a Subquery:

```sql
SELECT employee_id, first_name, last_name, salary 
FROM employees 
WHERE salary > (SELECT AVG(salary) FROM employees);
```

Here, the subquery `(SELECT AVG(salary) FROM employees)` calculates the average salary first, and then the outer query filters employees earning above that value.

---

### 2. Subqueries in the SELECT Clause (Column Expressions)

Subqueries can also be used in the `SELECT` clause to compute additional values for each row.

#### Problem:

Compare each employee's salary with the average salary.

#### Incorrect Attempt:

```sql
SELECT employee_id, salary, AVG(salary) AS average_salary FROM employees;
```

This results in an error because `AVG(salary)` requires a `GROUP BY` clause.

#### Correct Approach Using a Subquery:

```sql
SELECT employee_id, salary, 
       (SELECT AVG(salary) FROM employees) AS average_salary 
FROM employees;
```

Here, the subquery computes the overall average salary, making it available for each row in the outer query.

---

### 3. Subqueries in the FROM Clause (Derived Tables)

Subqueries can also act as temporary tables when placed in the `FROM` clause. These are known as derived tables or table expressions.

#### Problem:

Create a temporary table excluding sensitive employee details.

#### Approach Using a Derived Table:

```sql
SELECT * FROM 
    (SELECT employee_id, first_name, last_name, department_id FROM employees) AS employee_info;
```

In this example, the derived table `employee_info` contains only non-sensitive data, making it useful in scenarios requiring data abstraction.

---

### 4. Subqueries for Derived Tables with Aggregation

Subqueries can also be used to create derived tables, which can then be queried for specific insights.

#### Problem:

Find the average salary of the top 5 earners in the company.

#### Approach Using a Derived Table:

```sql
SELECT AVG(salary) 
FROM (SELECT salary 
      FROM employees 
      ORDER BY salary DESC 
      LIMIT 5) AS salary_table;
```

Here, the inner query extracts the top five salaries, and the outer query calculates their average. Note that it is necessary to give an alias (`salary_table`) to any derived tables.

---

## Summary

Subqueries enhance SQL queries in multiple ways:

1. **WHERE Clause** - Enables filtering using computed values.
2. **SELECT Clause (Column Expressions)** - Allows dynamic value generation for each row.
3. **FROM Clause (Derived Tables)** - Enables temporary data transformation before further processing.
4. **Derived Tables with Aggregation** - Allows querying specific subsets of data for further analysis.

By leveraging subqueries, we can construct more flexible and powerful SQL queries, overcoming limitations such as aggregate function constraints.

---

## Further Learning

To deepen your understanding, consider exploring:

- Common Table Expressions (CTEs) as an alternative to derived tables.
- Performance implications of subqueries vs. joins.
- Advanced use cases like correlated subqueries.

