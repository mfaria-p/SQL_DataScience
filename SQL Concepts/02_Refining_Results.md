# Using String Patterns, Ranges, Sets and Refining Results in SQL Queries

## Introduction
A Database Management System (DBMS) not only stores data but also facilitates efficient retrieval. The `SELECT` statement is fundamental for querying data from a database. While retrieving all rows is straightforward (`SELECT * FROM table_name`), filtering data using conditions is often necessary. This document explores how to simplify and optimize SQL queries using string patterns, ranges, sets, and grouping.

## String Patterns in SQL Queries
When filtering data using the `WHERE` clause, we often encounter scenarios where we only remember partial values. String patterns help retrieve data that match specific conditions.

### Using the `LIKE` Predicate
The `LIKE` predicate enables searching for patterns within text columns. It uses wildcard characters:
- `%` (percent sign) substitutes for zero or more characters.
- `_` (underscore) substitutes for a single character.

#### Example:
Retrieve authors whose first names start with 'R':
```sql
SELECT FirstName FROM Author
WHERE FirstName LIKE 'R%';
```
**Result Set:**
| FirstName |
|-----------|
| Raul      |
| Rav       |

### Using Multiple Wildcards
- Names ending with 'n': `LIKE '%n'`
- Names containing 'av': `LIKE '%av%'`

## Ranges in SQL Queries
A range condition simplifies filtering numeric data, especially when defining upper and lower bounds.

### Using `BETWEEN ... AND`
Instead of using multiple comparison operators (`>=`, `<=`), use the `BETWEEN` clause for readability.

#### Example:
Retrieve books with pages between 290 and 300:
```sql
SELECT Title FROM Book
WHERE Pages BETWEEN 290 AND 300;
```
This retrieves all books within the specified range (inclusive of 290 and 300).

## Using Sets in SQL Queries
For categorical data, the `IN` operator simplifies filtering against multiple values.

### Using `IN`
Instead of writing multiple `OR` conditions, `IN` allows a concise specification of required values.

#### Example:
Retrieve authors from specific countries:
```sql
SELECT AuthorName FROM Author
WHERE Country IN ('Canada', 'India', 'China');
```
This returns all authors from the specified countries without redundant conditions.

## Sorting Result Sets
Sorting data in a meaningful order improves readability and usability of query results.

### Using `ORDER BY`
By default, query results are not sorted in any particular order. The `ORDER BY` clause arranges data based on a specified column.

#### Example:
Sort books alphabetically by title:
```sql
SELECT Title FROM Book
ORDER BY Title;
```
This sorts the result set in **ascending** order (A to Z).

### Sorting in Descending Order
To sort results in descending order, add the `DESC` keyword.

#### Example:
Sort books in reverse alphabetical order:
```sql
SELECT Title FROM Book
ORDER BY Title DESC;
```

### Sorting by Column Position
Instead of specifying a column name, the column position in the `SELECT` statement can be used.

#### Example:
Sort books by page count using column position:
```sql
SELECT Title, Pages FROM Book
ORDER BY 2;
```
Since `Pages` is the second column in the result set, the sort order is based on it.

## Grouping Result Sets
Grouping data helps eliminate duplicates and summarize information.

### Eliminating Duplicates with `DISTINCT`
A `SELECT` statement result set can contain duplicate values. Use `DISTINCT` to remove duplicates.

#### Example:
Retrieve unique countries from the author table:
```sql
SELECT DISTINCT Country FROM Author;
```
This ensures each country appears only once in the result set.

### Using `GROUP BY`
The `GROUP BY` clause groups a result into subsets that have matching values for one or more columns.

#### Example:
Count the number of authors per country:
```sql
SELECT Country, COUNT(*) AS AuthorCount
FROM Author
GROUP BY Country;
```
This groups authors by country and counts the number of authors from each country.

### Filtering Groups with `HAVING`
The `HAVING` clause filters grouped data, similar to `WHERE` but applied after aggregation.

#### Example:
Retrieve only countries with more than four authors:
```sql
SELECT Country, COUNT(*) AS AuthorCount
FROM Author
GROUP BY Country
HAVING COUNT(*) > 4;
```
This returns only countries with five or more authors.

## Conclusion
By using:
- **String patterns (`LIKE` with wildcards)** for flexible text searches.
- **Range queries (`BETWEEN ... AND`)** for numeric filtering.
- **Set operators (`IN`)** for matching multiple values efficiently.
- **Sorting (`ORDER BY`)** for better-organized result sets.
- **Grouping (`GROUP BY` and `HAVING`)** for summarized data analysis.

We can write SQL queries that are concise, efficient, and easy to read.

