# Databases with Python and SQL

## Introduction

This module covers how to access databases using Python. Databases are powerful tools for data scientists, allowing for efficient data storage, retrieval, and analysis. By the end of this module, you will be able to:

- Explain the basic concepts of connecting Python applications to databases.
- Create tables, load data, and query data using SQL from Jupyter notebooks.
- Analyze data using Python.
- Connect to cloud-based databases and interact with them using SQL.

## Working with Databases in Python

There are three main ways to interact with databases using Python:
1. **Using DB-API**: Directly connect and execute SQL queries via Python’s built-in `sqlite3` module.
2. **Using SQL Magic**: Leverage Jupyter Notebook’s SQL extension for interactive querying.
3. **Using Pandas Library**: Read and write SQL tables as Pandas DataFrames for easy data manipulation.

### 1. Using DB-API in Python
The **DB-API** is Python’s standard API for accessing relational databases. It allows you to write code that interacts directly with databases using SQL commands.

#### Common DB-API Methods
| Method        | Syntax                     | Description |
|--------------|---------------------------|-------------|
| `connect()`  | `sqlite3.connect("db_name")` | Establishes a connection to a database. |
| `cursor()`   | `con.cursor()`             | Creates a cursor to execute SQL commands. |
| `execute()`  | `cursor.execute("SQL QUERY")` | Executes an SQL statement. |
| `fetchall()` | `cursor.fetchall()`        | Retrieves all rows from the query result. |
| `fetchmany()` | `cursor.fetchmany(n)`      | Retrieves a limited number of rows. |
| `close()`    | `con.close()`              | Closes the database connection. |

#### Example: Connecting to a SQLite Database
```python
import sqlite3

# Establish connection
con = sqlite3.connect("INSTRUCTOR.db")
cursor = con.cursor()

# Execute a query
cursor.execute("SELECT * FROM INSTRUCTOR")

# Fetch results
results = cursor.fetchall()
print(results)

# Close connection
con.close()
```

### 2. Using SQL Magic in Jupyter Notebooks
SQL Magic allows executing SQL queries directly in Jupyter notebooks.

#### Enabling SQL Magic
```python
%load_ext sql
%sql sqlite:///INSTRUCTOR.db
```

#### Running Queries
```sql
%%sql
SELECT * FROM INSTRUCTOR;
```

### 3. Using Pandas to Work with Databases
Pandas provides a seamless way to integrate databases with Python by reading SQL queries into DataFrames.

#### Common Pandas SQL Methods
| Method         | Syntax                      | Description |
|--------------|----------------------------|-------------|
| `read_csv()`  | `df = pd.read_csv("file.csv")` | Reads data from a CSV file into a DataFrame. |
| `read_sql()`  | `df = pd.read_sql("SQL QUERY", conn)` | Reads SQL query results into a DataFrame. |
| `to_sql()`    | `df.to_sql("table", conn, index=False)` | Writes a DataFrame into a database table. |

#### Example: Using Pandas to Query a Database
```python
import pandas as pd
import sqlite3

# Establish connection
conn = sqlite3.connect("INSTRUCTOR.db")

# Read data into DataFrame
df = pd.read_sql("SELECT * FROM INSTRUCTOR", conn)
print(df.head())

# Close connection
conn.close()
```

## Data Visualization with Seaborn
### Scatter Plots
Scatter plots show the relationship between two variables. We use `jointplot` from Seaborn to visualize correlations.

#### Example: Creating a Scatter Plot in Jupyter Notebook
```python
import matplotlib.pyplot as plt
%matplotlib inline
import seaborn as sns

income_vs_hardship = %sql SELECT per_capita_income_, hardship_index FROM chicago_socioeconomic_data;
plot = sns.jointplot(x='per_capita_income_', y='hardship_index', data=income_vs_hardship.DataFrame())
```

### Bar Plots
Bar plots visualize the relationship between categorical and numerical data.

```python
import seaborn as sns
sns.barplot(x='Test_Score', y='Frequency', data=df)
```

## Conclusion
By mastering Python and SQL for database access and visualization, you can efficiently manage and analyze data. The three main approaches—DB-API, SQL Magic, and Pandas—each offer unique advantages for interacting with databases in different scenarios.

