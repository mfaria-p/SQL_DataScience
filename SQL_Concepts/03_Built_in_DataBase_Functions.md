# Built-in Database Functions

## Introduction
While it is possible to fetch data from a database and perform operations on it within applications and notebooks, most databases come with built-in functions that allow operations to be performed directly in SQL statements. 

Using these functions can reduce network traffic, improve efficiency, and speed up processing, especially when dealing with large datasets. Additionally, databases support user-defined functions, which are an advanced topic beyond this lesson.

Here I will explore built-in SQL functions using the `PETRESCUE` table, which records rescue transactions, including columns such as `ID`, `ANIMAL`, `QUANTITY`, `COST`, and `RESCUE_DATE`.

---

## Aggregate (Column) Functions
Aggregate functions operate on a collection of values and return a single value or `NULL`. These functions include:

### 1. SUM Function
Calculates the total sum of values in a column.
```sql
SELECT SUM(COST) FROM PETRESCUE;
```
To assign a custom name to the output column:
```sql
SELECT SUM(COST) AS SUM_OF_COST FROM PETRESCUE;
```

### 2. MIN and MAX Functions
Find the minimum and maximum values in a column.
```sql
SELECT MIN(QUANTITY) FROM PETRESCUE;
SELECT MAX(QUANTITY) FROM PETRESCUE;
```
To get the minimum `ID` for dogs:
```sql
SELECT MIN(ID) FROM PETRESCUE WHERE ANIMAL = 'Dog';
```

### 3. AVG Function
Returns the average value of a column.
```sql
SELECT AVG(COST) FROM PETRESCUE;
```
To calculate the average cost per dog:
```sql
SELECT AVG(COST / QUANTITY) FROM PETRESCUE WHERE ANIMAL = 'Dog';
```

---

## Scalar and String Functions
Scalar functions operate on individual values, while string functions work specifically with text.

### 1. ROUND Function
Rounds numerical values to the nearest integer.
```sql
SELECT ROUND(COST) FROM PETRESCUE;
```

### 2. LENGTH Function
Returns the length of text values.
```sql
SELECT LENGTH(ANIMAL) FROM PETRESCUE;
```

### 3. UPPER and LOWER Functions
Convert text to uppercase or lowercase.
```sql
SELECT UPPER(ANIMAL) FROM PETRESCUE;
SELECT LOWER(ANIMAL) FROM PETRESCUE;
```
To match case-insensitive values:
```sql
SELECT * FROM PETRESCUE WHERE LOWER(ANIMAL) = 'cat';
```

### 4. DISTINCT and Nested Functions
Finds unique values, optionally transforming them.
```sql
SELECT DISTINCT(UPPER(ANIMAL)) FROM PETRESCUE;
```

---

## Date and Time Functions
Most databases contain special data types for handling dates and times, including `DATE`, `TIME`, and `TIMESTAMP`. These types follow specific formats:
- `DATE` (YYYYMMDD) - 8 digits
- `TIME` (HHMMSS) - 6 digits
- `TIMESTAMP` (YYYYXXDDHHMMSSZZZZZZ) - 20 digits, where `XX` represents the month and `ZZZZZZ` represents microseconds.

Functions exist to extract various date and time components:
- **Day, Month, Year**
- **Day of Month, Day of Week, Day of Year**
- **Week, Hour, Minute, Second**

### 1. Extracting Date Components
Extract the day portion of rescue dates for cats:
```sql
SELECT DAY(RESCUE_DATE) FROM PETRESCUE WHERE ANIMAL = 'Cat';
```

### 2. Using Date Functions in the WHERE Clause
Find the number of rescues in May:
```sql
SELECT COUNT(*) FROM PETRESCUE WHERE MONTH(RESCUE_DATE) = 5;
```

### 3. Performing Date Arithmetic
Find the date three days after each rescue date:
```sql
SELECT DATE_ADD(RESCUE_DATE, INTERVAL 3 DAY) FROM PETRESCUE;
```
Retrieve the date three days before each rescue date:
```sql
SELECT DATE_SUB(RESCUE_DATE, INTERVAL 3 DAY) FROM PETRESCUE;
```

### 4. Using Special Registers
Find the number of days passed since each rescue date:
```sql
SELECT DATEDIFF(CURRENT_DATE, RESCUE_DATE) FROM PETRESCUE;
```
To present the output in `YYYY-MM-DD` format:
```sql
SELECT FROM_DAYS(DATEDIFF(CURRENT_DATE, RESCUE_DATE)) FROM PETRESCUE;
```

### 5. Calculating Age
To calculate the age of an individual or an entity based on a birth date:
```sql
SELECT YEAR(FROM_DAYS(DATEDIFF(CURRENT_DATE, B_DATE))) AS AGE FROM EMPLOYEES;
```
This query computes the difference in days between the current date and the birth date, converts it into a date format, and extracts the year, effectively returning the age in years.

---

## Conclusion
This guide covered SQL aggregate functions such as `SUM`, `MIN`, `MAX`, and `AVG`, along with scalar and string functions like `ROUND`, `LOWER`, and `UPPER`. We also explored date and time functions, including extracting date components, performing arithmetic, and using special registers. Utilizing these built-in functions can optimize database queries and improve performance when working with structured data.

