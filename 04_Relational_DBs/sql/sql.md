# SQL

SQL (Structured Query Language) is a standard programming language for managing and manipulating databases. It is used to query, insert, update, and delete data in relational databases.


### Basic SQL and Database Terminologies

1. **Database**:
   - A structured collection of data stored electronically. Examples include MySQL, PostgreSQL, SQLite, and Microsoft SQL Server.

2. **Table**:
   - A collection of related data entries consisting of rows and columns. Each table has a unique name.

3. **Row**:
   - Also known as a record or tuple, a row in a table represents a single data item. Each row contains data corresponding to one entry.

4. **Column**:
   - Also known as a field or attribute, a column in a table represents a data type or a specific category of data (e.g., name, age, address). Each column has a unique name.

5. **Primary Key**:
   - A column or set of columns that uniquely identifies each row in a table. Each table can have only one primary key.

6. **Foreign Key**:
   - A column or set of columns that establishes a relationship between two tables. A foreign key in one table points to a primary key in another table.

7. **Index**:
   - A database object that improves the speed of data retrieval operations on a table at the cost of additional storage space.

8. **Query**:
   - A request for data or information from a database. SQL queries are written to perform operations like retrieving, inserting, updating, and deleting data.

9. **SQL (Structured Query Language)**:
   - A standard programming language for managing and manipulating databases.

10. **Schema**:
    - The structure or organization of a database, defined by tables, columns, relationships, views, indexes, and other database objects.

11. **Data Types**:
    - The types of data that can be stored in a column. Common data types include INTEGER, VARCHAR (variable character), DATE, and BOOLEAN.

12. **Constraints**:
    - Rules applied to columns to enforce data integrity and accuracy. Examples include NOT NULL, UNIQUE, PRIMARY KEY, and FOREIGN KEY.

13. **DDL (Data Definition Language)**:
    - SQL commands used to define and manage database objects, such as CREATE, ALTER, and DROP.

14. **DML (Data Manipulation Language)**:
    - SQL commands used to manipulate data within database objects, such as SELECT, INSERT, UPDATE, and DELETE.

15. **JOIN**:
    - An operation used to combine rows from two or more tables based on a related column between them. Types include INNER JOIN, LEFT JOIN, RIGHT JOIN, and FULL JOIN.

16. **Normalization**:
    - The process of organizing data in a database to reduce redundancy and improve data integrity. It involves dividing large tables into smaller ones and defining relationships between them.

17. **Transaction**:
    - A sequence of one or more SQL operations treated as a single unit. Transactions ensure data integrity and consistency, with properties defined by ACID (Atomicity, Consistency, Isolation, Durability).

18. **View**:
    - A virtual table created by a query. A view does not store data itself but provides a way to look at data from one or more tables.

### Example

Here’s a small example to illustrate some of these concepts:

```sql
-- Create a table called 'Users'
CREATE TABLE Users (
    UserID INT PRIMARY KEY,         -- Primary Key
    UserName VARCHAR(100) NOT NULL, -- Not Null Constraint
    Email VARCHAR(100) UNIQUE       -- Unique Constraint
);

-- Insert data into 'Users' table
INSERT INTO Users (UserID, UserName, Email)
VALUES (1, 'Alice', 'alice@example.com'),
       (2, 'Bob', 'bob@example.com');

-- Select data from 'Users' table
SELECT * FROM Users;

-- Create another table called 'Orders' with a Foreign Key
CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    OrderDate DATE,
    UserID INT,
    FOREIGN KEY (UserID) REFERENCES Users(UserID) -- Foreign Key Constraint
);

-- Insert data into 'Orders' table
INSERT INTO Orders (OrderID, OrderDate, UserID)
VALUES (101, '2023-06-01', 1),
       (102, '2023-06-02', 2);

-- Select data from 'Orders' table
SELECT * FROM Orders;

-- Join 'Users' and 'Orders' tables to get user names with their orders
SELECT Users.UserName, Orders.OrderDate
FROM Users
JOIN Orders ON Users.UserID = Orders.UserID;
```

----------------------------------------------


The `SELECT` statement, one of the most fundamental and widely used SQL commands. The `SELECT` statement is used to query and retrieve data from a database. Here are the key components and variations of the `SELECT` statement:

### Basic `SELECT` Statement

The simplest form of the `SELECT` statement retrieves all columns from a table:

```sql
SELECT * FROM table_name;
```

- `SELECT`: Specifies the columns to retrieve.
- `*`: A wildcard that means "all columns."
- `FROM table_name`: Specifies the table to retrieve data from.

### Selecting Specific Columns

To retrieve specific columns, list the column names separated by commas:

```sql
SELECT column1, column2 FROM table_name;
```

### Using the `WHERE` Clause

The `WHERE` clause filters the results based on specified conditions:

```sql
SELECT column1, column2 FROM table_name WHERE condition;
```

For example:

```sql
SELECT UserName, Email FROM Users WHERE UserID = 1;
```

### Using Logical Operators

You can combine multiple conditions using logical operators like `AND`, `OR`, and `NOT`:

```sql
SELECT column1, column2
FROM table_name
WHERE condition1 AND condition2;
```

Example:

```sql
SELECT UserName, Email FROM Users WHERE UserID = 1 OR UserName = 'Bob';
```

### Sorting Results with `ORDER BY`

The `ORDER BY` clause sorts the results by one or more columns:

```sql
SELECT column1, column2
FROM table_name
ORDER BY column1 [ASC|DESC], column2 [ASC|DESC];
```

- `ASC`: Ascending order (default).
- `DESC`: Descending order.

Example:

```sql
SELECT UserName, Email FROM Users ORDER BY UserName ASC;
```

### Limiting Results with `LIMIT`

The `LIMIT` clause restricts the number of rows returned:

```sql
SELECT column1, column2
FROM table_name
LIMIT number_of_rows;
```

Example:

```sql
SELECT UserName, Email FROM Users LIMIT 2;
```

### Using Aggregate Functions

Aggregate functions perform calculations on a set of values and return a single value. Common aggregate functions include `COUNT`, `SUM`, `AVG`, `MIN`, and `MAX`:

```sql
SELECT COUNT(*) FROM Users;
```

### Grouping Results with `GROUP BY`

The `GROUP BY` clause groups rows that have the same values in specified columns into summary rows:

```sql
SELECT column1, COUNT(*)
FROM table_name
GROUP BY column1;
```

Example:

```sql
SELECT UserID, COUNT(*) AS OrderCount
FROM Orders
GROUP BY UserID;
```

### Filtering Groups with `HAVING`

The `HAVING` clause is used to filter groups based on aggregate functions:

```sql
SELECT column1, COUNT(*)
FROM table_name
GROUP BY column1
HAVING COUNT(*) > value;
```

Example:

```sql
SELECT UserID, COUNT(*) AS OrderCount
FROM Orders
GROUP BY UserID
HAVING COUNT(*) > 1;
```

### Example Database

Let’s use a simple example database with two tables: `Users` and `Orders`.

#### Users Table

| UserID | UserName | Email             |
|--------|----------|-------------------|
| 1      | Alice    | alice@example.com |
| 2      | Bob      | bob@example.com   |

#### Orders Table

| OrderID | OrderDate   | UserID |
|---------|-------------|--------|
| 101     | 2023-06-01  | 1      |
| 102     | 2023-06-02  | 2      |
| 103     | 2023-06-03  | 1      |

### Example Queries

1. **Retrieve all users**:

   ```sql
   SELECT * FROM Users;
   ```

2. **Retrieve specific columns**:

   ```sql
   SELECT UserName, Email FROM Users;
   ```

3. **Filter results**:

   ```sql
   SELECT UserName, Email FROM Users WHERE UserID = 1;
   ```

4. **Sort results**:

   ```sql
   SELECT UserName, Email FROM Users ORDER BY UserName ASC;
   ```

5. **Limit results**:

   ```sql
   SELECT UserName, Email FROM Users LIMIT 1;
   ```

6. **Count orders per user**:

   ```sql
   SELECT UserID, COUNT(*) AS OrderCount
   FROM Orders
   GROUP BY UserID;
   ```

7. **Filter groups with `HAVING`**:

   ```sql
   SELECT UserID, COUNT(*) AS OrderCount
   FROM Orders
   GROUP BY UserID
   HAVING COUNT(*) > 1;
   ```

These are the basics of the `SELECT` statement. Practicing these queries will help you get comfortable with retrieving and manipulating data from a database.

------------------

The `SELECT DISTINCT` statement in SQL is used to return only distinct (unique) values in the result set. It eliminates duplicate records from the results of a query.

### Syntax

```sql
SELECT DISTINCT column1, column2, ...
FROM table_name;
```

### Explanation
- `DISTINCT`: Keyword used to remove duplicates.
- `column1, column2, ...`: The columns from which you want to retrieve distinct values.
- `table_name`: The table from which to retrieve data.

### Example Usage

Let's consider a table `Orders` with the following data:

| OrderID | OrderDate   | UserID |
|---------|-------------|--------|
| 101     | 2023-06-01  | 1      |
| 102     | 2023-06-02  | 2      |
| 103     | 2023-06-01  | 1      |
| 104     | 2023-06-03  | 3      |

#### Example 1: Select Distinct UserID

To get a list of unique `UserID` values from the `Orders` table:

```sql
SELECT DISTINCT UserID FROM Orders;
```

Result:

| UserID |
|--------|
| 1      |
| 2      |
| 3      |

#### Example 2: Select Distinct OrderDate

To get a list of unique `OrderDate` values from the `Orders` table:

```sql
SELECT DISTINCT OrderDate FROM Orders;
```

Result:

| OrderDate  |
|------------|
| 2023-06-01 |
| 2023-06-02 |
| 2023-06-03 |

#### Example 3: Select Distinct Combination of Columns

To get a list of unique combinations of `UserID` and `OrderDate` from the `Orders` table:

```sql
SELECT DISTINCT UserID, OrderDate FROM Orders;
```

Result:

| UserID | OrderDate   |
|--------|-------------|
| 1      | 2023-06-01  |
| 2      | 2023-06-02  |
| 3      | 2023-06-03  |

### Practical Use Case

Consider a scenario where you have a table `Customers` with the following data:

| CustomerID | FirstName | LastName   | City        |
|------------|-----------|------------|-------------|
| 1          | Alice     | Johnson    | New York    |
| 2          | Bob       | Smith      | Los Angeles |
| 3          | Alice     | Johnson    | New York    |
| 4          | Charlie   | Brown      | Chicago     |

#### Example 4: Select Distinct Cities

To get a list of unique cities where customers live:

```sql
SELECT DISTINCT City FROM Customers;
```

Result:

| City        |
|-------------|
| New York    |
| Los Angeles |
| Chicago     |

#### Example 5: Select Distinct First and Last Names

To get a list of unique combinations of first and last names:

```sql
SELECT DISTINCT FirstName, LastName FROM Customers;
```

Result:

| FirstName | LastName |
|-----------|----------|
| Alice     | Johnson  |
| Bob       | Smith    |
| Charlie   | Brown    |

### Notes

- The `DISTINCT` keyword applies to all columns listed in the `SELECT` statement. If any combination of the listed columns is unique in the result set, it will be included in the results.
- Using `DISTINCT` can impact query performance, especially on large tables, as the database must compare all selected fields to identify and remove duplicates.

Using `SELECT DISTINCT` is a powerful way to eliminate duplicate data and ensure that your result set contains only unique records.


-------------------------
The `WHERE` clause in SQL is used to filter records and retrieve only those that meet specified conditions. It allows you to define criteria for selecting rows from a table.

### WHERE clause Syntax

```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```

### Explanation
- `SELECT column1, column2, ...`: Specifies the columns to retrieve.
- `FROM table_name`: Specifies the table to retrieve data from.
- `WHERE condition`: Specifies the condition that each row must meet to be included in the result set.

### Operators Used in the `WHERE` Clause

1. **Comparison Operators**:
   - `=`: Equal to
   - `<>` or `!=`: Not equal to
   - `>`: Greater than
   - `<`: Less than
   - `>=`: Greater than or equal to
   - `<=`: Less than or equal to

2. **Logical Operators**:
   - `AND`: Combines two conditions. Both must be true.
   - `OR`: Combines two conditions. At least one must be true.
   - `NOT`: Negates a condition.

3. **BETWEEN**:
   - Checks if a value is within a range.

   ```sql
   column BETWEEN value1 AND value2
   ```

4. **IN**:
   - Checks if a value is within a set of values.

   ```sql
   column IN (value1, value2, ...)
   ```

5. **LIKE**:
   - Searches for a pattern in a column.

   ```sql
   column LIKE pattern
   ```

6. **IS NULL**:
   - Checks if a column is NULL.

   ```sql
   column IS NULL
   ```

### Example Usage

Consider the following `Users` table:

| UserID | UserName | Email             | Age | City        |
|--------|----------|-------------------|-----|-------------|
| 1      | Alice    | alice@example.com | 30  | New York    |
| 2      | Bob      | bob@example.com   | 25  | Los Angeles |
| 3      | Charlie  | charlie@example.com | 35 | Chicago     |
| 4      | David    | david@example.com | 28  | New York    |
| 5      | Eve      | eve@example.com   | 22  | Los Angeles |

#### Example 1: Simple Condition

Retrieve users who live in New York:

```sql
SELECT UserName, Email FROM Users WHERE City = 'New York';
```

Result:

| UserName | Email             |
|----------|-------------------|
| Alice    | alice@example.com |
| David    | david@example.com |

#### Example 2: Multiple Conditions with `AND`

Retrieve users who live in New York and are older than 25:

```sql
SELECT UserName, Email FROM Users WHERE City = 'New York' AND Age > 25;
```

Result:

| UserName | Email             |
|----------|-------------------|
| Alice    | alice@example.com |

#### Example 3: Multiple Conditions with `OR`

Retrieve users who live in New York or are older than 30:

```sql
SELECT UserName, Email FROM Users WHERE City = 'New York' OR Age > 30;
```

Result:

| UserName | Email               |
|----------|---------------------|
| Alice    | alice@example.com   |
| Charlie  | charlie@example.com |
| David    | david@example.com   |

#### Example 4: Using `BETWEEN`

Retrieve users aged between 25 and 30:

```sql
SELECT UserName, Email FROM Users WHERE Age BETWEEN 25 AND 30;
```

Result:

| UserName | Email             |
|----------|-------------------|
| Alice    | alice@example.com |
| Bob      | bob@example.com   |
| David    | david@example.com |

#### Example 5: Using `IN`

Retrieve users who live in New York or Los Angeles:

```sql
SELECT UserName, Email FROM Users WHERE City IN ('New York', 'Los Angeles');
```

Result:

| UserName | Email             |
|----------|-------------------|
| Alice    | alice@example.com |
| Bob      | bob@example.com   |
| David    | david@example.com |
| Eve      | eve@example.com   |

#### Example 6: Using `LIKE`

Retrieve users whose name starts with 'A':

```sql
SELECT UserName, Email FROM Users WHERE UserName LIKE 'A%';
```

Result:

| UserName | Email             |
|----------|-------------------|
| Alice    | alice@example.com |

#### Example 7: Using `IS NULL`

Consider a `Users` table where some emails are NULL:

| UserID | UserName | Email             | Age | City        |
|--------|----------|-------------------|-----|-------------|
| 1      | Alice    | alice@example.com | 30  | New York    |
| 2      | Bob      | NULL              | 25  | Los Angeles |
| 3      | Charlie  | charlie@example.com | 35 | Chicago     |
| 4      | David    | NULL              | 28  | New York    |
| 5      | Eve      | eve@example.com   | 22  | Los Angeles |

Retrieve users whose email is NULL:

```sql
SELECT UserName FROM Users WHERE Email IS NULL;
```

Result:

| UserName |
|----------|
| Bob      |
| David    |

These examples cover the basics of using the `WHERE` clause to filter data in SQL queries. By combining different conditions and operators, you can create powerful and flexible queries to extract exactly the data you need.

--------------------------------------------------

The `ORDER BY` keyword in SQL is used to sort the result set of a query by one or more columns. By default, the sorting is in ascending order, but you can specify descending order if needed.

### ORDER BY keyword Syntax

```sql
SELECT column1, column2, ...
FROM table_name
ORDER BY column1 [ASC|DESC], column2 [ASC|DESC], ...;
```

### Explanation
- `ORDER BY`: Keyword used to sort the result set.
- `column1, column2, ...`: The columns by which to sort the data.
- `ASC`: Sorts the data in ascending order (default).
- `DESC`: Sorts the data in descending order.

### Example Usage

Consider the following `Users` table:

| UserID | UserName | Email             | Age | City        |
|--------|----------|-------------------|-----|-------------|
| 1      | Alice    | alice@example.com | 30  | New York    |
| 2      | Bob      | bob@example.com   | 25  | Los Angeles |
| 3      | Charlie  | charlie@example.com | 35 | Chicago     |
| 4      | David    | david@example.com | 28  | New York    |
| 5      | Eve      | eve@example.com   | 22  | Los Angeles |

#### Example 1: Sort by a Single Column in Ascending Order

Retrieve all users sorted by `UserName` in ascending order:

```sql
SELECT UserName, Email, Age, City FROM Users ORDER BY UserName ASC;
```

Result:

| UserName | Email             | Age | City        |
|----------|-------------------|-----|-------------|
| Alice    | alice@example.com | 30  | New York    |
| Bob      | bob@example.com   | 25  | Los Angeles |
| Charlie  | charlie@example.com | 35 | Chicago     |
| David    | david@example.com | 28  | New York    |
| Eve      | eve@example.com   | 22  | Los Angeles |

#### Example 2: Sort by a Single Column in Descending Order

Retrieve all users sorted by `Age` in descending order:

```sql
SELECT UserName, Email, Age, City FROM Users ORDER BY Age DESC;
```

Result:

| UserName | Email               | Age | City        |
|----------|---------------------|-----|-------------|
| Charlie  | charlie@example.com | 35  | Chicago     |
| Alice    | alice@example.com   | 30  | New York    |
| David    | david@example.com   | 28  | New York    |
| Bob      | bob@example.com     | 25  | Los Angeles |
| Eve      | eve@example.com     | 22  | Los Angeles |

#### Example 3: Sort by Multiple Columns

Retrieve all users sorted by `City` in ascending order and then by `Age` in descending order:

```sql
SELECT UserName, Email, Age, City FROM Users ORDER BY City ASC, Age DESC;
```

Result:

| UserName | Email               | Age | City        |
|----------|---------------------|-----|-------------|
| Charlie  | charlie@example.com | 35  | Chicago     |
| Alice    | alice@example.com   | 30  | New York    |
| David    | david@example.com   | 28  | New York    |
| Bob      | bob@example.com     | 25  | Los Angeles |
| Eve      | eve@example.com     | 22  | Los Angeles |

#### Example 4: Sort by an Alias

If you use an alias in your `SELECT` statement, you can sort by that alias as well. For example:

```sql
SELECT UserName, Email, Age AS UserAge, City FROM Users ORDER BY UserAge ASC;
```

Result:

| UserName | Email               | UserAge | City        |
|----------|---------------------|---------|-------------|
| Eve      | eve@example.com     | 22      | Los Angeles |
| Bob      | bob@example.com     | 25      | Los Angeles |
| David    | david@example.com   | 28      | New York    |
| Alice    | alice@example.com   | 30      | New York    |
| Charlie  | charlie@example.com | 35      | Chicago     |

### Practical Use Case

Consider a scenario where you have a `Products` table with the following data:

| ProductID | ProductName | Price | Category   |
|-----------|-------------|-------|------------|
| 1         | Laptop      | 1200  | Electronics|
| 2         | Smartphone  | 800   | Electronics|
| 3         | Chair       | 150   | Furniture  |
| 4         | Desk        | 300   | Furniture  |
| 5         | Headphones  | 100   | Electronics|

#### Example 5: Sort Products by Category and Price

Retrieve all products sorted by `Category` in ascending order and then by `Price` in descending order:

```sql
SELECT ProductName, Price, Category FROM Products ORDER BY Category ASC, Price DESC;
```

Result:

| ProductName | Price | Category   |
|-------------|-------|------------|
| Laptop      | 1200  | Electronics|
| Smartphone  | 800   | Electronics|
| Headphones  | 100   | Electronics|
| Desk        | 300   | Furniture  |
| Chair       | 150   | Furniture  |

### Notes

- Sorting by multiple columns can help in organizing data in a more meaningful way, especially when dealing with complex datasets.
- The performance of the `ORDER BY` clause can be impacted by the size of the dataset and the number of columns being sorted. Using indexes on the columns involved in the `ORDER BY` can improve performance.

Using the `ORDER BY` keyword effectively allows you to present data in a sorted and organized manner, making it easier to analyze and understand. 

----------------------------------

In SQL, the `AND`, `OR`, and `NOT` operators are used to combine multiple conditions in the `WHERE` clause. These logical operators help in creating complex queries to filter data more precisely.

### `AND` Operator

The `AND` operator combines two conditions and returns true only if both conditions are true.

#### Syntax

```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition1 AND condition2;
```

#### Example

Consider the `Users` table:

| UserID | UserName | Email               | Age | City        |
|--------|----------|---------------------|-----|-------------|
| 1      | Alice    | alice@example.com   | 30  | New York    |
| 2      | Bob      | bob@example.com     | 25  | Los Angeles |
| 3      | Charlie  | charlie@example.com | 35  | Chicago     |
| 4      | David    | david@example.com   | 28  | New York    |
| 5      | Eve      | eve@example.com     | 22  | Los Angeles |

Retrieve users who live in New York and are older than 25:

```sql
SELECT UserName, Email, Age, City
FROM Users
WHERE City = 'New York' AND Age > 25;
```

Result:

| UserName | Email             | Age | City     |
|----------|-------------------|-----|----------|
| Alice    | alice@example.com | 30  | New York |

### `OR` Operator

The `OR` operator combines two conditions and returns true if at least one of the conditions is true.

#### Syntax

```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition1 OR condition2;
```

#### Example

Retrieve users who live in New York or are older than 30:

```sql
SELECT UserName, Email, Age, City
FROM Users
WHERE City = 'New York' OR Age > 30;
```

Result:

| UserName | Email               | Age | City     |
|----------|---------------------|-----|----------|
| Alice    | alice@example.com   | 30  | New York |
| Charlie  | charlie@example.com | 35  | Chicago  |
| David    | david@example.com   | 28  | New York |

### `NOT` Operator

The `NOT` operator negates a condition, returning true if the condition is false and vice versa.

#### Syntax

```sql
SELECT column1, column2, ...
FROM table_name
WHERE NOT condition;
```

#### Example

Retrieve users who do not live in New York:

```sql
SELECT UserName, Email, Age, City
FROM Users
WHERE NOT City = 'New York';
```

Result:

| UserName | Email               | Age | City        |
|----------|---------------------|-----|-------------|
| Bob      | bob@example.com     | 25  | Los Angeles |
| Charlie  | charlie@example.com | 35  | Chicago     |
| Eve      | eve@example.com     | 22  | Los Angeles |

### Combining `AND`, `OR`, and `NOT`

You can combine these operators to create more complex conditions. Use parentheses `()` to group conditions and control the order of evaluation.

#### Example

Retrieve users who live in New York and are either older than 25 or have the name 'David':

```sql
SELECT UserName, Email, Age, City
FROM Users
WHERE City = 'New York' AND (Age > 25 OR UserName = 'David');
```

Result:

| UserName | Email             | Age | City     |
|----------|-------------------|-----|----------|
| Alice    | alice@example.com | 30  | New York |
| David    | david@example.com | 28  | New York |

### Practical Example

Consider a `Products` table:

| ProductID | ProductName | Price | Category   |
|-----------|-------------|-------|------------|
| 1         | Laptop      | 1200  | Electronics|
| 2         | Smartphone  | 800   | Electronics|
| 3         | Chair       | 150   | Furniture  |
| 4         | Desk        | 300   | Furniture  |
| 5         | Headphones  | 100   | Electronics|

#### Example 1: Using `AND` Operator

Retrieve products in the 'Electronics' category that cost more than $500:

```sql
SELECT ProductName, Price, Category
FROM Products
WHERE Category = 'Electronics' AND Price > 500;
```

Result:

| ProductName | Price | Category    |
|-------------|-------|-------------|
| Laptop      | 1200  | Electronics |
| Smartphone  | 800   | Electronics |

#### Example 2: Using `OR` Operator

Retrieve products in the 'Furniture' category or products that cost less than $200:

```sql
SELECT ProductName, Price, Category
FROM Products
WHERE Category = 'Furniture' OR Price < 200;
```

Result:

| ProductName | Price | Category    |
|-------------|-------|-------------|
| Chair       | 150   | Furniture   |
| Desk        | 300   | Furniture   |
| Headphones  | 100   | Electronics |

#### Example 3: Using `NOT` Operator

Retrieve products that are not in the 'Electronics' category:

```sql
SELECT ProductName, Price, Category
FROM Products
WHERE NOT Category = 'Electronics';
```

Result:

| ProductName | Price | Category |
|-------------|-------|----------|
| Chair       | 150   | Furniture|
| Desk        | 300   | Furniture|

#### Example 4: Combining `AND`, `OR`, and `NOT`

Retrieve products that are in the 'Electronics' category and either cost less than $200 or have 'Laptop' in the name:

```sql
SELECT ProductName, Price, Category
FROM Products
WHERE Category = 'Electronics' AND (Price < 200 OR ProductName = 'Laptop');
```

Result:

| ProductName | Price | Category    |
|-------------|-------|-------------|
| Laptop      | 1200  | Electronics |
| Headphones  | 100   | Electronics |

These examples illustrate how you can use the `AND`, `OR`, and `NOT` operators to create complex query conditions in SQL.

-------------------------------

The `INSERT INTO` statement in SQL is used to insert new rows of data into a table. You can specify the columns for which you want to insert data, or you can insert values into all columns if you provide values for each.

### Syntax

#### Insert into Specific Columns

```sql
INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);
```

#### Insert into All Columns

```sql
INSERT INTO table_name
VALUES (value1, value2, value3, ...);
```

### Example Usage

Consider the following `Users` table:

| UserID | UserName | Email               | Age | City        |
|--------|----------|---------------------|-----|-------------|
| 1      | Alice    | alice@example.com   | 30  | New York    |
| 2      | Bob      | bob@example.com     | 25  | Los Angeles |
| 3      | Charlie  | charlie@example.com | 35  | Chicago     |

#### Example 1: Insert into Specific Columns

Insert a new user specifying the columns:

```sql
INSERT INTO Users (UserName, Email, Age, City)
VALUES ('David', 'david@example.com', 28, 'New York');
```

After this operation, the `Users` table will be:

| UserID | UserName | Email               | Age | City        |
|--------|----------|---------------------|-----|-------------|
| 1      | Alice    | alice@example.com   | 30  | New York    |
| 2      | Bob      | bob@example.com     | 25  | Los Angeles |
| 3      | Charlie  | charlie@example.com | 35  | Chicago     |
| 4      | David    | david@example.com   | 28  | New York    |

#### Example 2: Insert into All Columns

Insert a new user providing values for all columns (including `UserID`):

```sql
INSERT INTO Users
VALUES (5, 'Eve', 'eve@example.com', 22, 'Los Angeles');
```

After this operation, the `Users` table will be:

| UserID | UserName | Email               | Age | City        |
|--------|----------|---------------------|-----|-------------|
| 1      | Alice    | alice@example.com   | 30  | New York    |
| 2      | Bob      | bob@example.com     | 25  | Los Angeles |
| 3      | Charlie  | charlie@example.com | 35  | Chicago     |
| 4      | David    | david@example.com   | 28  | New York    |
| 5      | Eve      | eve@example.com     | 22  | Los Angeles |

### Practical Use Case

Consider a `Products` table with the following structure:

| ProductID | ProductName | Price | Category   |
|-----------|-------------|-------|------------|
| 1         | Laptop      | 1200  | Electronics|
| 2         | Smartphone  | 800   | Electronics|
| 3         | Chair       | 150   | Furniture  |

#### Example 3: Insert a New Product

Insert a new product into the `Products` table:

```sql
INSERT INTO Products (ProductName, Price, Category)
VALUES ('Desk', 300, 'Furniture');
```

After this operation, the `Products` table will be:

| ProductID | ProductName | Price | Category   |
|-----------|-------------|-------|------------|
| 1         | Laptop      | 1200  | Electronics|
| 2         | Smartphone  | 800   | Electronics|
| 3         | Chair       | 150   | Furniture  |
| 4         | Desk        | 300   | Furniture  |

### Notes

1. **Auto-increment Columns**: If a table has an auto-increment column (e.g., `UserID`), you do not need to insert a value into that column; the database will automatically generate it. For example:
   
   ```sql
   INSERT INTO Users (UserName, Email, Age, City)
   VALUES ('Frank', 'frank@example.com', 40, 'Chicago');
   ```

2. **Default Values**: If a column has a default value and you do not provide a value for that column, the default value will be used.

3. **Inserting Multiple Rows**: You can insert multiple rows in a single `INSERT` statement by separating the rows with commas:
   
   ```sql
   INSERT INTO Users (UserName, Email, Age, City)
   VALUES 
   ('George', 'george@example.com', 45, 'San Francisco'),
   ('Hannah', 'hannah@example.com', 32, 'Boston');
   ```

   This inserts both `George` and `Hannah` into the `Users` table.

Using the `INSERT INTO` statement allows you to add new data to your tables, making it a fundamental operation in managing a database.

---------------------------------
In SQL, `NULL` is a special marker used to indicate that a data value does not exist in the database. `NULL` is not the same as an empty string or a zero value; it represents the absence of any value.

### Key Points about `NULL`

1. **NULL is not equal to anything, even itself**:
   - A comparison with `NULL` using standard comparison operators (like `=`, `<>`, etc.) will always yield `UNKNOWN` rather than `TRUE` or `FALSE`.
   
2. **NULL Handling**:
   - To test for `NULL`, use the `IS NULL` or `IS NOT NULL` operators.

3. **NULL in Functions**:
   - Most functions return `NULL` when given a `NULL` input.

### Checking for `NULL` Values

#### Using `IS NULL`

To check for `NULL` values in a column:

```sql
SELECT column1, column2, ...
FROM table_name
WHERE column_name IS NULL;
```

#### Using `IS NOT NULL`

To check for non-`NULL` values in a column:

```sql
SELECT column1, column2, ...
FROM table_name
WHERE column_name IS NOT NULL;
```

### Example Usage

Consider the following `Users` table with some `NULL` values:

| UserID | UserName | Email             | Age | City        |
|--------|----------|-------------------|-----|-------------|
| 1      | Alice    | alice@example.com | 30  | New York    |
| 2      | Bob      | NULL              | 25  | Los Angeles |
| 3      | Charlie  | charlie@example.com | NULL | Chicago   |
| 4      | David    | david@example.com | 28  | NULL        |
| 5      | Eve      | eve@example.com   | 22  | Los Angeles |

#### Example 1: Find Rows with `NULL` Values

Retrieve users with `NULL` email addresses:

```sql
SELECT UserID, UserName, Email
FROM Users
WHERE Email IS NULL;
```

Result:

| UserID | UserName | Email |
|--------|----------|-------|
| 2      | Bob      | NULL  |

#### Example 2: Find Rows without `NULL` Values

Retrieve users with non-`NULL` cities:

```sql
SELECT UserID, UserName, City
FROM Users
WHERE City IS NOT NULL;
```

Result:

| UserID | UserName | City        |
|--------|----------|-------------|
| 1      | Alice    | New York    |
| 2      | Bob      | Los Angeles |
| 3      | Charlie  | Chicago     |
| 5      | Eve      | Los Angeles |

### Functions and `NULL`

Many SQL functions handle `NULL` values in specific ways. Here are a few examples:

#### `COALESCE` Function

The `COALESCE` function returns the first non-`NULL` value in a list of expressions.

```sql
SELECT UserID, UserName, COALESCE(Email, 'No Email') AS Email
FROM Users;
```

Result:

| UserID | UserName | Email           |
|--------|----------|-----------------|
| 1      | Alice    | alice@example.com |
| 2      | Bob      | No Email        |
| 3      | Charlie  | charlie@example.com |
| 4      | David    | david@example.com |
| 5      | Eve      | eve@example.com |

#### `IFNULL` or `ISNULL` Function

Some SQL dialects (like MySQL) provide `IFNULL` or `ISNULL` functions to handle `NULL` values. They work similarly to `COALESCE`.

In MySQL:

```sql
SELECT UserID, UserName, IFNULL(Email, 'No Email') AS Email
FROM Users;
```

In SQL Server:

```sql
SELECT UserID, UserName, ISNULL(Email, 'No Email') AS Email
FROM Users;
```

### Aggregating with `NULL`

When using aggregate functions, `NULL` values are typically ignored.

#### Example: Counting Rows

Count the number of users, including those with `NULL` values:

```sql
SELECT COUNT(*) AS TotalUsers
FROM Users;
```

Result:

| TotalUsers |
|------------|
| 5          |

Count the number of users with non-`NULL` email addresses:

```sql
SELECT COUNT(Email) AS UsersWithEmail
FROM Users;
```

Result:

| UsersWithEmail |
|----------------|
| 4              |

### Practical Example

Consider a `Products` table where some descriptions are `NULL`:

| ProductID | ProductName | Description       | Price | Category   |
|-----------|-------------|-------------------|-------|------------|
| 1         | Laptop      | High performance  | 1200  | Electronics|
| 2         | Smartphone  | NULL              | 800   | Electronics|
| 3         | Chair       | Comfortable       | 150   | Furniture  |
| 4         | Desk        | NULL              | 300   | Furniture  |
| 5         | Headphones  | Noise cancelling  | 100   | Electronics|

#### Example 1: Find Products with `NULL` Descriptions

```sql
SELECT ProductID, ProductName
FROM Products
WHERE Description IS NULL;
```

Result:

| ProductID | ProductName |
|-----------|-------------|
| 2         | Smartphone  |
| 4         | Desk        |

#### Example 2: Provide a Default Description

```sql
SELECT ProductID, ProductName, COALESCE(Description, 'No Description') AS Description
FROM Products;
```

Result:

| ProductID | ProductName | Description       |
|-----------|-------------|-------------------|
| 1         | Laptop      | High performance  |
| 2         | Smartphone  | No Description    |
| 3         | Chair       | Comfortable       |
| 4         | Desk        | No Description    |
| 5         | Headphones  | Noise cancelling  |

Understanding how to work with `NULL` values is crucial for accurate data handling and analysis in SQL.


### `UPDATE` and `DELETE` statements in SQL:

1. **UPDATE Statement**: This statement is used to modify existing records in a table. The basic syntax is:

   ```sql
   UPDATE table_name
   SET column1 = value1, column2 = value2, ...
   WHERE condition;
   ```

   - `table_name`: The name of the table you want to update.
   - `SET`: Specifies the columns to be updated and the new values they should be given.
   - `WHERE`: Specifies which rows to update. If omitted, all rows will be updated.

   Example:

   ```sql
   UPDATE employees
   SET salary = 50000
   WHERE department = 'Sales';
   ```

   This would update the `salary` column to 50000 for all employees in the 'Sales' department.

2. **DELETE Statement**: This statement is used to remove records from a table. The basic syntax is:

   ```sql
   DELETE FROM table_name
   WHERE condition;
   ```

   - `table_name`: The name of the table from which you want to delete records.
   - `WHERE`: Specifies which rows to delete. If omitted, all rows will be deleted.

   Example:

   ```sql
   DELETE FROM customers
   WHERE age < 18;
   ```

   This would delete all records from the `customers` table where the age is less than 18.

Both `UPDATE` and `DELETE` statements should be used with caution, especially the `DELETE` statement as it permanently removes records from a table. Always ensure you have a backup and are confident in the conditions you use in your `WHERE` clauses to avoid unintentional data loss.


--------------------------------

The `TOP`, `LIMIT`, `FETCH FIRST`, and `ROWNUM` clauses are used in SQL to limit the number of rows returned by a query. However, their usage may vary slightly depending on the specific SQL dialect you're using (e.g., SQL Server, MySQL, PostgreSQL, Oracle).

1. **TOP (SQL Server)**: The `TOP` clause is used in SQL Server to specify the number of rows to return from the beginning of a result set. The basic syntax is:

   ```sql
   SELECT TOP (expression) column1, column2, ...
   FROM table_name
   WHERE condition;
   ```

   Example:

   ```sql
   SELECT TOP 5 * 
   FROM employees
   ORDER BY salary DESC;
   ```

   This query retrieves the top 5 highest paid employees from the `employees` table.

2. **LIMIT (MySQL / PostgreSQL)**: The `LIMIT` clause is used in MySQL and PostgreSQL to limit the number of rows returned by a query. The basic syntax is:

   ```sql
   SELECT column1, column2, ...
   FROM table_name
   WHERE condition
   LIMIT number_of_rows;
   ```

   Example (MySQL):

   ```sql
   SELECT *
   FROM orders
   LIMIT 10;
   ```

   This query retrieves the first 10 rows from the `orders` table.

3. **FETCH FIRST (ANSI SQL, IBM Db2)**: The `FETCH FIRST` clause is part of the ANSI SQL standard and is also supported by IBM Db2. It's used to limit the number of rows returned by a query. The basic syntax is:

   ```sql
   SELECT column1, column2, ...
   FROM table_name
   WHERE condition
   FETCH FIRST number_of_rows ROWS ONLY;
   ```

   Example:

   ```sql
   SELECT *
   FROM products
   ORDER BY price
   FETCH FIRST 3 ROWS ONLY;
   ```

   This query retrieves the top 3 cheapest products from the `products` table.

4. **ROWNUM (Oracle)**: The `ROWNUM` pseudo-column is used in Oracle to limit the number of rows returned by a query. The basic syntax is:

   ```sql
   SELECT column1, column2, ...
   FROM table_name
   WHERE condition
   AND ROWNUM <= number_of_rows;
   ```

   Example:

   ```sql
   SELECT *
   FROM customers
   WHERE ROWNUM <= 100;
   ```

   This query retrieves the first 100 rows from the `customers` table.

These clauses are handy for pagination or when you only need a subset of the data from a table.


SQL aggregate functions are used to perform calculations on sets of rows to give a single result. Here are some common aggregate functions:

1. **COUNT**: Returns the number of rows that match a specified condition.
   
   Example:
   ```sql
   SELECT COUNT(*) FROM employees;
   ```

2. **SUM**: Returns the sum of values in a numeric column.
   
   Example:
   ```sql
   SELECT SUM(salary) FROM employees;
   ```

3. **AVG**: Returns the average value of a numeric column.
   
   Example:
   ```sql
   SELECT AVG(salary) FROM employees;
   ```

4. **MIN**: Returns the smallest value in a column.
   
   Example:
   ```sql
   SELECT MIN(salary) FROM employees;
   ```

5. **MAX**: Returns the largest value in a column.
   
   Example:
   ```sql
   SELECT MAX(salary) FROM employees;
   ```

6. **GROUP BY**: Groups rows that have the same values into summary rows, typically used with aggregate functions to perform calculations per group.
   
   Example:
   ```sql
   SELECT department, AVG(salary) 
   FROM employees
   GROUP BY department;
   ```

7. **HAVING**: Allows you to filter groups of rows returned by a GROUP BY clause.
   
   Example:
   ```sql
   SELECT department, AVG(salary) 
   FROM employees
   GROUP BY department
   HAVING AVG(salary) > 50000;
   ```

Aggregate functions are powerful tools for summarizing and analyzing data in SQL queries, especially when dealing with large datasets.