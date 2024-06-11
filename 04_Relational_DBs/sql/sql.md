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


### LIKE operator

The `LIKE` operator in SQL is used to search for a specified pattern in a column. It is commonly used in the `WHERE` clause of a `SELECT`, `UPDATE`, or `DELETE` statement. The `LIKE` operator is often combined with wildcard characters to create flexible pattern-matching searches.

### Wildcard Characters

1. **% (Percent Sign)**: Represents zero, one, or multiple characters.
2. **_ (Underscore)**: Represents a single character.

### Syntax

```sql
SELECT column1, column2, ...
FROM table_name
WHERE column LIKE pattern;
```

### Examples

1. **Using % Wildcard**

   To find all customers whose names start with 'A':
   ```sql
   SELECT * FROM customers
   WHERE name LIKE 'A%';
   ```
   This query retrieves all rows where the `name` starts with 'A'.

2. **Using _ Wildcard**

   To find all customers whose names have 'a' as the second character:
   ```sql
   SELECT * FROM customers
   WHERE name LIKE '_a%';
   ```
   This query retrieves all rows where the `name` has 'a' as the second character.

3. **Combining % and _ Wildcards**

   To find all customers whose names start with 'A' and have exactly three characters:
   ```sql
   SELECT * FROM customers
   WHERE name LIKE 'A__';
   ```
   This query retrieves all rows where the `name` starts with 'A' and is exactly three characters long.

4. **Using % Wildcard for Substring Search**

   To find all products containing the word 'chair':
   ```sql
   SELECT * FROM products
   WHERE description LIKE '%chair%';
   ```
   This query retrieves all rows where the `description` contains 'chair' anywhere within the text.

5. **Using NOT LIKE**

   To find all customers whose names do not start with 'A':
   ```sql
   SELECT * FROM customers
   WHERE name NOT LIKE 'A%';
   ```
   This query retrieves all rows where the `name` does not start with 'A'.

### Case Sensitivity

- **SQL Server**: Case sensitivity depends on the collation settings of the database.
- **MySQL**: The `LIKE` operator is case-insensitive by default, but can be made case-sensitive using the `BINARY` keyword.
  
  Example:
  ```sql
  SELECT * FROM customers
  WHERE name LIKE BINARY 'a%';
  ```

- **PostgreSQL**: By default, the `LIKE` operator is case-sensitive. Use `ILIKE` for case-insensitive pattern matching.

  Example:
  ```sql
  SELECT * FROM customers
  WHERE name ILIKE 'a%';
  ```

The `LIKE` operator is a powerful tool for pattern matching and searching within text data, offering flexibility through the use of wildcards.


## SQL wildcard characters

SQL wildcard characters are used with the `LIKE` operator to search for patterns in text data. Here are the primary wildcard characters and their uses:

1. **Percent Sign (%)**: Represents zero, one, or multiple characters. It is used to search for a sequence of characters.

   Examples:
   - `'%abc'`: Matches any string that ends with 'abc'.
   - `'abc%'`: Matches any string that starts with 'abc'.
   - `'%abc%'`: Matches any string that contains 'abc'.

   ```sql
   SELECT * FROM employees WHERE name LIKE 'A%';
   ```

   This query retrieves all employees whose names start with 'A'.

2. **Underscore (_)**: Represents a single character. It is used to search for strings with a specific pattern of characters.

   Examples:
   - `'a_c'`: Matches any three-character string that starts with 'a' and ends with 'c'.
   - `'__a'`: Matches any three-character string that ends with 'a'.

   ```sql
   SELECT * FROM employees WHERE name LIKE '_a_';
   ```

   This query retrieves all employees whose names have 'a' as the second character.

3. **Square Brackets ([])**: Used to specify a set or range of characters. (SQL Server)

   Examples:
   - `'a[bcd]e'`: Matches 'abe', 'ace', or 'ade'.
   - `'t[aeiou]n'`: Matches 'tan', 'ten', 'tin', 'ton', or 'tun'.

   ```sql
   SELECT * FROM employees WHERE name LIKE 'J[oa]n';
   ```

   This query retrieves all employees whose names are 'Jan' or 'Jon'.

4. **Caret (^)**: Used inside square brackets to specify characters that should not be matched. (SQL Server)

   Example:
   - `'t[^aeiou]n'`: Matches 'tbn', 'tcn', etc., but not 'tan', 'ten', 'tin', 'ton', or 'tun'.

   ```sql
   SELECT * FROM employees WHERE name LIKE 'J[^oa]n';
   ```

   This query retrieves all employees whose names do not have 'o' or 'a' as the second character, like 'Jen' or 'Jim'.

5. **Hyphen (-)**: Used inside square brackets to specify a range of characters. (SQL Server)

   Example:
   - `'a[a-z]c'`: Matches any three-character string that starts with 'a', ends with 'c', and has any lowercase letter in the middle.

   ```sql
   SELECT * FROM employees WHERE name LIKE '[A-C]%';
   ```

   This query retrieves all employees whose names start with 'A', 'B', or 'C'.

### Examples

1. **Finding Names Starting with a Specific Letter**

   ```sql
   SELECT * FROM customers WHERE name LIKE 'S%';
   ```
   This retrieves all customers whose names start with 'S'.

2. **Finding Names Ending with a Specific Letter**

   ```sql
   SELECT * FROM customers WHERE name LIKE '%n';
   ```

   This retrieves all customers whose names end with 'n'.

3. **Finding Names with a Specific Pattern**

   ```sql
   SELECT * FROM customers WHERE name LIKE '_a%';
   ```

   This retrieves all customers whose names have 'a' as the second character.

4. **Finding Names Containing a Specific Substring**

   ```sql
   SELECT * FROM customers WHERE name LIKE '%ann%';
   ```

   This retrieves all customers whose names contain 'ann'.

### Notes

- **Case Sensitivity**: The behavior of the `LIKE` operator with regard to case sensitivity depends on the SQL dialect and the collation settings of the database.
  - **SQL Server**: Case sensitivity depends on the collation settings.
  - **MySQL**: `LIKE` is case-insensitive by default, but can be made case-sensitive using the `BINARY` keyword.
  - **PostgreSQL**: `LIKE` is case-sensitive by default; use `ILIKE` for case-insensitive searches.

By using these wildcard characters effectively, you can perform powerful and flexible pattern matching in SQL queries.


### `IN` operator

The `IN` operator in SQL is used to specify multiple values in a `WHERE` clause. It allows you to filter records based on whether a column's value matches any value in a specified list. This operator is a convenient way to combine multiple `OR` conditions into a single, more readable query.

### Syntax

```sql
SELECT column1, column2, ...
FROM table_name
WHERE column_name IN (value1, value2, ...);
```

### Examples

1. **Basic Usage**

   To find all employees whose department is either 'Sales', 'Marketing', or 'HR':

   ```sql
   SELECT * FROM employees
   WHERE department IN ('Sales', 'Marketing', 'HR');
   ```

   This query retrieves all rows where the `department` column matches any of the specified values.

2. **With Numeric Values**

   To find all orders with IDs 1, 2, or 3:

   ```sql
   SELECT * FROM orders
   WHERE order_id IN (1, 2, 3);
   ```

   This query retrieves all rows where the `order_id` column is either 1, 2, or 3.

3. **With Subquery**

   The `IN` operator can also be used with a subquery to filter records based on the result of another query. For example, to find all employees who are in departments that have more than 10 employees:

   ```sql
   SELECT * FROM employees
   WHERE department_id IN (
       SELECT department_id
       FROM departments
       WHERE employee_count > 10
   );
   ```

   This query retrieves all employees who work in departments with more than 10 employees.

4. **NOT IN**

   The `NOT IN` operator is used to exclude records that match any value in a specified list. For example, to find all employees whose department is not 'Sales', 'Marketing', or 'HR':

   ```sql
   SELECT * FROM employees
   WHERE department NOT IN ('Sales', 'Marketing', 'HR');
   ```

   This query retrieves all rows where the `department` column does not match any of the specified values.

### Performance Considerations

- **Large Lists**: Using the `IN` operator with very large lists can impact performance. In such cases, consider alternative approaches such as joining with a temporary table.
- **Indexes**: The performance of the `IN` operator can be improved by ensuring that the column being filtered is indexed.
- **Subqueries**: When using subqueries with `IN`, ensure that the subquery is efficient and returns a manageable number of results.

### Example Scenarios

1. **Filter by Multiple Criteria**

   To find products that are either in category 1, 2, or 3 and are priced above $50:

   ```sql
   SELECT * FROM products
   WHERE category_id IN (1, 2, 3) AND price > 50;
   ```

2. **Combining `IN` with Other Conditions**

   To find customers from specific cities who have placed more than 5 orders:

   ```sql
   SELECT * FROM customers
   WHERE city IN ('New York', 'Los Angeles', 'Chicago')
   AND order_count > 5;
   ```

3. **Using `IN` with Strings**

   To find all books authored by 'John Doe', 'Jane Smith', or 'Emily Johnson':

   ```sql
   SELECT * FROM books
   WHERE author IN ('John Doe', 'Jane Smith', 'Emily Johnson');
   ```

The `IN` operator is a powerful tool for simplifying SQL queries that involve multiple conditions, making your code more readable and maintainable.


### `BETWEEN` operator

The `BETWEEN` operator in SQL is used to filter the result set within a certain range. The range is inclusive, meaning it includes both the start and end values. This operator can be used with numeric, date, and text data types.

### Syntax

```sql
SELECT column1, column2, ...
FROM table_name
WHERE column_name BETWEEN value1 AND value2;
```

### Examples

1. **Numeric Range**

   To find all employees with salaries between 30,000 and 70,000:

   ```sql
   SELECT * FROM employees
   WHERE salary BETWEEN 30000 AND 70000;
   ```

   This query retrieves all rows where the `salary` column is between 30,000 and 70,000, inclusive.

2. **Date Range**

   To find all orders placed between January 1, 2023, and December 31, 2023:

   ```sql
   SELECT * FROM orders
   WHERE order_date BETWEEN '2023-01-01' AND '2023-12-31';
   ```

   This query retrieves all rows where the `order_date` column falls within the specified date range.

3. **Text Range**

   To find all products whose names are alphabetically between 'Apple' and 'Orange':

   ```sql
   SELECT * FROM products
   WHERE product_name BETWEEN 'Apple' AND 'Orange';
   ```

   This query retrieves all rows where the `product_name` column falls alphabetically between 'Apple' and 'Orange'.

### Using `NOT BETWEEN`

The `NOT BETWEEN` operator is used to exclude a range of values.

To find all employees with salaries not between 30,000 and 70,000:

```sql
SELECT * FROM employees
WHERE salary NOT BETWEEN 30000 AND 70000;
```

This query retrieves all rows where the `salary` column is outside the range of 30,000 and 70,000.

### Combining `BETWEEN` with Other Conditions

You can combine the `BETWEEN` operator with other conditions using `AND` or `OR` operators.

To find all employees with salaries between 30,000 and 70,000 who work in the 'Sales' department:

```sql
SELECT * FROM employees
WHERE salary BETWEEN 30000 AND 70000
AND department = 'Sales';
```

### Performance Considerations

- **Indexes**: Using `BETWEEN` on indexed columns can improve query performance.
- **Data Type Compatibility**: Ensure the data types of the column and the range values are compatible to avoid errors or unexpected results.
- **Inclusive Nature**: Remember that the `BETWEEN` operator includes the start and end values in the result set.

### Example Scenarios

1. **Finding Records Within a Range of Dates**

   To find all bookings made in the first quarter of 2023:

   ```sql
   SELECT * FROM bookings
   WHERE booking_date BETWEEN '2023-01-01' AND '2023-03-31';
   ```

2. **Filtering Numeric Data Within a Range**

   To find products priced between $10 and $50:

   ```sql
   SELECT * FROM products
   WHERE price BETWEEN 10 AND 50;
   ```

3. **Filtering Text Data Within a Range**

   To find employees with last names starting between 'A' and 'M':

   ```sql
   SELECT * FROM employees
   WHERE last_name BETWEEN 'A' AND 'M';
   ```

The `BETWEEN` operator is a straightforward and efficient way to filter data within a specified range, making your SQL queries concise and readable.

### SQL aliases

SQL aliases are used to give a table or a column in a query a temporary name. Aliases make column names more readable and can simplify complex queries. They are especially useful when dealing with long or complex table and column names, or when joining multiple tables.

### Syntax

**Column Alias**

```sql
SELECT column_name AS alias_name
FROM table_name;
```

**Table Alias**

```sql
SELECT column_name
FROM table_name AS alias_name;
```

### Examples

1. **Column Alias**

   To make the output of a column more readable:

   ```sql
   SELECT first_name AS FirstName, last_name AS LastName
   FROM employees;
   ```

   This query retrieves the `first_name` and `last_name` columns from the `employees` table and displays them as `FirstName` and `LastName`, respectively.

2. **Table Alias**

   To simplify table names in a query, especially when joining tables:

   ```sql
   SELECT e.first_name, e.last_name, d.department_name
   FROM employees AS e
   JOIN departments AS d ON e.department_id = d.department_id;
   ```

   In this query, `employees` is aliased as `e` and `departments` as `d`. This makes the query easier to read and write, especially when dealing with multiple joins or complex conditions.

3. **Combining Column and Table Aliases**

   ```sql
   SELECT e.first_name AS FirstName, e.last_name AS LastName, d.department_name AS Department
   FROM employees AS e
   JOIN departments AS d ON e.department_id = d.department_id;
   ```

   This query combines both column and table aliases to make the query more readable and the result set more understandable.

### Aliases Without the `AS` Keyword

The `AS` keyword is optional when creating an alias. The following query is equivalent to the previous one:

```sql
SELECT e.first_name FirstName, e.last_name LastName, d.department_name Department
FROM employees e
JOIN departments d ON e.department_id = d.department_id;
```

### Using Aliases in Aggregations and Calculations

1. **Aggregations**

   To use an alias with an aggregate function:

   ```sql
   SELECT department_id, COUNT(*) AS EmployeeCount
   FROM employees
   GROUP BY department_id;
   ```

   This query counts the number of employees in each department and labels the count as `EmployeeCount`.

2. **Calculations**

   To use an alias in a calculation:

   ```sql
   SELECT product_name, price, price * 0.1 AS Tax
   FROM products;
   ```

   This query calculates 10% tax on the price of each product and labels the result as `Tax`.

### Example Scenarios

1. **Complex Queries with Joins**

   To join multiple tables and simplify the query using aliases:

   ```sql
   SELECT o.order_id, c.customer_name, p.product_name, o.quantity
   FROM orders o
   JOIN customers c ON o.customer_id = c.customer_id
   JOIN products p ON o.product_id = p.product_id;
   ```

2. **Subqueries with Aliases**

   To use aliases in subqueries:

   ```sql
   SELECT e.first_name, e.last_name, dept.Department
   FROM employees e
   JOIN (SELECT department_id, department_name AS Department FROM departments) dept
   ON e.department_id = dept.department_id;
   ```

### Best Practices

- **Clarity**: Use aliases to make column and table names clearer and more meaningful.
- **Consistency**: Be consistent in your use of aliases to improve readability and maintainability of your queries.
- **Avoid Conflicts**: Ensure that alias names do not conflict with existing column or table names in your database.

SQL aliases are powerful tools for simplifying and clarifying your queries, making them easier to write, read, and maintain.


### SQL joins
SQL joins are used to combine records from two or more tables based on a related column between them. Here is an overview of the different types of joins and their usage:

### 1. INNER JOIN

The `INNER JOIN` keyword selects records that have matching values in both tables.

**Syntax:**
```sql
SELECT columns
FROM table1
INNER JOIN table2 ON table1.common_column = table2.common_column;
```

**Example:**
```sql
SELECT employees.first_name, employees.last_name, departments.department_name
FROM employees
INNER JOIN departments ON employees.department_id = departments.department_id;
```
This query retrieves employees' first and last names along with their corresponding department names, but only for those employees who have a department.

### 2. LEFT (OUTER) JOIN

The `LEFT JOIN` keyword returns all records from the left table (table1), and the matched records from the right table (table2). The result is NULL from the right side if there is no match.

**Syntax:**
```sql
SELECT columns
FROM table1
LEFT JOIN table2 ON table1.common_column = table2.common_column;
```

**Example:**
```sql
SELECT employees.first_name, employees.last_name, departments.department_name
FROM employees
LEFT JOIN departments ON employees.department_id = departments.department_id;
```
This query retrieves all employees' first and last names, and their department names if available. For employees without a department, the department name will be NULL.

### 3. RIGHT (OUTER) JOIN

The `RIGHT JOIN` keyword returns all records from the right table (table2), and the matched records from the left table (table1). The result is NULL from the left side if there is no match.

**Syntax:**
```sql
SELECT columns
FROM table1
RIGHT JOIN table2 ON table1.common_column = table2.common_column;
```

**Example:**
```sql
SELECT employees.first_name, employees.last_name, departments.department_name
FROM employees
RIGHT JOIN departments ON employees.department_id = departments.department_id;
```
This query retrieves all departments and the employees working in them. For departments without employees, the employee details will be NULL.

### 4. FULL (OUTER) JOIN

The `FULL JOIN` keyword returns all records when there is a match in either left (table1) or right (table2) table records. It returns NULL for non-matching rows from both tables.

**Syntax:**
```sql
SELECT columns
FROM table1
FULL JOIN table2 ON table1.common_column = table2.common_column;
```

**Example:**
```sql
SELECT employees.first_name, employees.last_name, departments.department_name
FROM employees
FULL JOIN departments ON employees.department_id = departments.department_id;
```

This query retrieves all employees and departments, showing the employees with their departments, and including departments and employees with no matches.

### 5. CROSS JOIN

The `CROSS JOIN` keyword returns the Cartesian product of the two tables, meaning it returns all possible combinations of rows.

**Syntax:**
```sql
SELECT columns
FROM table1
CROSS JOIN table2;
```

**Example:**
```sql
SELECT employees.first_name, departments.department_name
FROM employees
CROSS JOIN departments;
```
This query retrieves all combinations of employees' first names and department names.

### 6. SELF JOIN

A `SELF JOIN` is a regular join but the table is joined with itself.

**Syntax:**
```sql
SELECT a.columns, b.columns
FROM table a, table b
WHERE condition;
```

**Example:**
```sql
SELECT a.employee_id, a.first_name AS EmployeeName, b.first_name AS ManagerName
FROM employees a
JOIN employees b ON a.manager_id = b.employee_id;
```
This query retrieves employees along with their manager's name by joining the `employees` table with itself.

### Example Scenarios

1. **INNER JOIN with Additional Conditions**
   ```sql
   SELECT employees.first_name, employees.last_name, departments.department_name
   FROM employees
   INNER JOIN departments ON employees.department_id = departments.department_id
   WHERE employees.salary > 50000;
   ```

2. **LEFT JOIN with Aggregation**
   ```sql
   SELECT departments.department_name, COUNT(employees.employee_id) AS EmployeeCount
   FROM departments
   LEFT JOIN employees ON departments.department_id = employees.department_id
   GROUP BY departments.department_name;
   ```

3. **RIGHT JOIN with Filtering**
   ```sql
   SELECT employees.first_name, employees.last_name, departments.department_name
   FROM employees
   RIGHT JOIN departments ON employees.department_id = departments.department_id
   WHERE departments.location = 'New York';
   ```

4. **FULL JOIN with Null Handling**
   ```sql
   SELECT COALESCE(employees.first_name, 'No Employee') AS EmployeeName,
          COALESCE(departments.department_name, 'No Department') AS DepartmentName
   FROM employees
   FULL JOIN departments ON employees.department_id = departments.department_id;
   ```

### Best Practices

- **Understand Join Types**: Choose the appropriate join type based on the relationship and desired result.
- **Use Aliases**: Use table aliases for readability and to avoid column name conflicts.
- **Performance**: Be mindful of performance, especially with large datasets and complex joins. Indexing can improve join performance.

By understanding and using these join types appropriately, you can effectively query and analyze data across multiple related tables in your database.


### `GROUP BY` Statement

The `GROUP BY` statement in SQL is used to arrange identical data into groups. It is often used with aggregate functions (`COUNT`, `MAX`, `MIN`, `SUM`, `AVG`) to perform operations on each group of data.

### Syntax

```sql
SELECT column1, aggregate_function(column2)
FROM table_name
WHERE condition
GROUP BY column1, column3, ...;
```

### Examples

1. **Basic Usage**

   To find the number of employees in each department:

   ```sql
   SELECT department_id, COUNT(employee_id) AS NumberOfEmployees
   FROM employees
   GROUP BY department_id;
   ```

   This query groups the employees by `department_id` and counts the number of employees in each department.

2. **Using Multiple Columns**

   To find the number of employees in each department and each job title:

   ```sql
   SELECT department_id, job_title, COUNT(employee_id) AS NumberOfEmployees
   FROM employees
   GROUP BY department_id, job_title;
   ```

   This query groups the employees by both `department_id` and `job_title`, and counts the number of employees in each combination.

3. **With Aggregate Functions**

   To find the average salary in each department:

   ```sql
   SELECT department_id, AVG(salary) AS AverageSalary
   FROM employees
   GROUP BY department_id;
   ```

   This query groups the employees by `department_id` and calculates the average salary in each department.

4. **Using `HAVING` Clause**

   The `HAVING` clause is used to filter groups based on a condition, similar to how the `WHERE` clause is used to filter rows.

   To find departments with more than 10 employees:

   ```sql
   SELECT department_id, COUNT(employee_id) AS NumberOfEmployees
   FROM employees
   GROUP BY department_id
   HAVING COUNT(employee_id) > 10;
   ```

   This query groups the employees by `department_id` and only includes departments with more than 10 employees.

### Example Scenarios

1. **Summarizing Sales by Product**

   To find the total sales amount for each product:

   ```sql
   SELECT product_id, SUM(sales_amount) AS TotalSales
   FROM sales
   GROUP BY product_id;
   ```

2. **Counting Customers by City**

   To find the number of customers in each city:

   ```sql
   SELECT city, COUNT(customer_id) AS NumberOfCustomers
   FROM customers
   GROUP BY city;
   ```

3. **Finding Maximum Salary by Department**

   To find the highest salary in each department:

   ```sql
   SELECT department_id, MAX(salary) AS MaxSalary
   FROM employees
   GROUP BY department_id;
   ```

4. **Filtering Groups with `HAVING` Clause**

   To find departments where the average salary is greater than 60,000:

   ```sql
   SELECT department_id, AVG(salary) AS AverageSalary
   FROM employees
   GROUP BY department_id
   HAVING AVG(salary) > 60000;
   ```

### Important Points

- **Grouping Columns**: All columns in the `SELECT` statement that are not used within an aggregate function must be included in the `GROUP BY` clause.
- **`HAVING` vs. `WHERE`**: The `WHERE` clause filters rows before grouping, while the `HAVING` clause filters groups after grouping.
- **Performance**: Grouping large datasets can be resource-intensive. Proper indexing can help improve performance.

### Complex Example

To find the total sales amount for each product category and the average sales amount for categories with total sales greater than 50,000:

```sql
SELECT product_category, SUM(sales_amount) AS TotalSales, AVG(sales_amount) AS AverageSales
FROM sales
GROUP BY product_category
HAVING SUM(sales_amount) > 50000;
```

This query groups the sales data by `product_category`, calculates the total and average sales amount for each category, and only includes categories where the total sales amount is greater than 50,000.

The `GROUP BY` statement is essential for summarizing and aggregating data in SQL, making it a powerful tool for data analysis and reporting.

### `HAVING` clause

The `HAVING` clause in SQL is used to filter groups of data created by the `GROUP BY` clause. It is similar to the `WHERE` clause, but the `WHERE` clause is used to filter rows before grouping, while the `HAVING` clause is used to filter groups after grouping. The `HAVING` clause is often used with aggregate functions.

### Syntax

```sql
SELECT column1, aggregate_function(column2)
FROM table_name
WHERE condition
GROUP BY column1
HAVING aggregate_function(column2) condition;
```

### Examples

1. **Basic Usage**

   To find departments with more than 10 employees:

   ```sql
   SELECT department_id, COUNT(employee_id) AS NumberOfEmployees
   FROM employees
   GROUP BY department_id
   HAVING COUNT(employee_id) > 10;
   ```

   This query groups the employees by `department_id` and includes only those departments with more than 10 employees.

2. **Using Multiple Aggregate Functions**

   To find departments where the total salary is greater than 100,000 and the average salary is greater than 30,000:

   ```sql
   SELECT department_id, SUM(salary) AS TotalSalary, AVG(salary) AS AverageSalary
   FROM employees
   GROUP BY department_id
   HAVING SUM(salary) > 100000 AND AVG(salary) > 30000;
   ```

   This query groups the employees by `department_id` and includes only those departments where the total salary exceeds 100,000 and the average salary exceeds 30,000.

3. **Using `HAVING` with `GROUP BY` and `ORDER BY`**

   To find the top 3 departments with the highest average salary, where the average salary is above 50,000:

   ```sql
   SELECT department_id, AVG(salary) AS AverageSalary
   FROM employees
   GROUP BY department_id
   HAVING AVG(salary) > 50000
   ORDER BY AverageSalary DESC
   LIMIT 3;
   ```

   This query groups the employees by `department_id`, filters out departments with an average salary of 50,000 or less, and then orders the result by average salary in descending order, returning only the top 3 departments.

### Example Scenarios

1. **Filtering Groups with Aggregated Data**

   To find products with total sales above 500 units:

   ```sql
   SELECT product_id, SUM(quantity) AS TotalSales
   FROM sales
   GROUP BY product_id
   HAVING SUM(quantity) > 500;
   ```

2. **Combining `HAVING` with `WHERE`**

   To find customers who have placed more than 5 orders and have a total spending of more than 1000:

   ```sql
   SELECT customer_id, COUNT(order_id) AS NumberOfOrders, SUM(total_amount) AS TotalSpending
   FROM orders
   WHERE order_status = 'completed'
   GROUP BY customer_id
   HAVING COUNT(order_id) > 5 AND SUM(total_amount) > 1000;
   ```

   This query first filters completed orders with the `WHERE` clause, then groups the results by `customer_id`, and finally applies the `HAVING` clause to include only those customers who meet both conditions.

3. **Using `HAVING` with Non-Aggregate Columns**

   To find employees in specific departments who have a total salary greater than 200,000:

   ```sql
   SELECT department_id, job_title, SUM(salary) AS TotalSalary
   FROM employees
   WHERE department_id IN (1, 2, 3)
   GROUP BY department_id, job_title
   HAVING SUM(salary) > 200000;
   ```

   This query filters employees in departments 1, 2, and 3, groups them by `department_id` and `job_title`, and includes only those groups where the total salary exceeds 200,000.

### Important Points

- **Order of Execution**: The `HAVING` clause is evaluated after the `GROUP BY` clause but before the `ORDER BY` clause.
- **Aggregate Functions**: The `HAVING` clause typically includes aggregate functions like `COUNT`, `SUM`, `AVG`, `MAX`, `MIN`.
- **Combining with `WHERE`**: Use the `WHERE` clause to filter rows before grouping and the `HAVING` clause to filter groups after grouping.

### Complex Example

To find the average and total sales amount for each product category and include only those categories with total sales greater than 50,000, ordering the result by average sales in descending order:

```sql
SELECT product_category, AVG(sales_amount) AS AverageSales, SUM(sales_amount) AS TotalSales
FROM sales
GROUP BY product_category
HAVING SUM(sales_amount) > 50000
ORDER BY AverageSales DESC;
```

This query groups the sales data by `product_category`, calculates the average and total sales amount for each category, filters out categories with total sales of 50,000 or less, and orders the result by average sales in descending order.

The `HAVING` clause is a powerful tool for filtering groups of data in SQL, allowing you to perform more detailed and specific data analysis.


The `HAVING` clause in SQL is used to filter groups of data created by the `GROUP BY` clause. It is similar to the `WHERE` clause, but the `WHERE` clause is used to filter rows before grouping, while the `HAVING` clause is used to filter groups after grouping. The `HAVING` clause is often used with aggregate functions.

### Syntax

```sql
SELECT column1, aggregate_function(column2)
FROM table_name
WHERE condition
GROUP BY column1
HAVING aggregate_function(column2) condition;
```

### Examples

1. **Basic Usage**

   To find departments with more than 10 employees:

   ```sql
   SELECT department_id, COUNT(employee_id) AS NumberOfEmployees
   FROM employees
   GROUP BY department_id
   HAVING COUNT(employee_id) > 10;
   ```

   This query groups the employees by `department_id` and includes only those departments with more than 10 employees.

2. **Using Multiple Aggregate Functions**

   To find departments where the total salary is greater than 100,000 and the average salary is greater than 30,000:

   ```sql
   SELECT department_id, SUM(salary) AS TotalSalary, AVG(salary) AS AverageSalary
   FROM employees
   GROUP BY department_id
   HAVING SUM(salary) > 100000 AND AVG(salary) > 30000;
   ```

   This query groups the employees by `department_id` and includes only those departments where the total salary exceeds 100,000 and the average salary exceeds 30,000.

3. **Using `HAVING` with `GROUP BY` and `ORDER BY`**

   To find the top 3 departments with the highest average salary, where the average salary is above 50,000:

   ```sql
   SELECT department_id, AVG(salary) AS AverageSalary
   FROM employees
   GROUP BY department_id
   HAVING AVG(salary) > 50000
   ORDER BY AverageSalary DESC
   LIMIT 3;
   ```

   This query groups the employees by `department_id`, filters out departments with an average salary of 50,000 or less, and then orders the result by average salary in descending order, returning only the top 3 departments.

### Example Scenarios

1. **Filtering Groups with Aggregated Data**

   To find products with total sales above 500 units:

   ```sql
   SELECT product_id, SUM(quantity) AS TotalSales
   FROM sales
   GROUP BY product_id
   HAVING SUM(quantity) > 500;
   ```

2. **Combining `HAVING` with `WHERE`**

   To find customers who have placed more than 5 orders and have a total spending of more than 1000:

   ```sql
   SELECT customer_id, COUNT(order_id) AS NumberOfOrders, SUM(total_amount) AS TotalSpending
   FROM orders
   WHERE order_status = 'completed'
   GROUP BY customer_id
   HAVING COUNT(order_id) > 5 AND SUM(total_amount) > 1000;
   ```

   This query first filters completed orders with the `WHERE` clause, then groups the results by `customer_id`, and finally applies the `HAVING` clause to include only those customers who meet both conditions.

3. **Using `HAVING` with Non-Aggregate Columns**

   To find employees in specific departments who have a total salary greater than 200,000:

   ```sql
   SELECT department_id, job_title, SUM(salary) AS TotalSalary
   FROM employees
   WHERE department_id IN (1, 2, 3)
   GROUP BY department_id, job_title
   HAVING SUM(salary) > 200000;
   ```

   This query filters employees in departments 1, 2, and 3, groups them by `department_id` and `job_title`, and includes only those groups where the total salary exceeds 200,000.

### Important Points

- **Order of Execution**: The `HAVING` clause is evaluated after the `GROUP BY` clause but before the `ORDER BY` clause.
- **Aggregate Functions**: The `HAVING` clause typically includes aggregate functions like `COUNT`, `SUM`, `AVG`, `MAX`, `MIN`.
- **Combining with `WHERE`**: Use the `WHERE` clause to filter rows before grouping and the `HAVING` clause to filter groups after grouping.

### Complex Example

To find the average and total sales amount for each product category and include only those categories with total sales greater than 50,000, ordering the result by average sales in descending order:

```sql
SELECT product_category, AVG(sales_amount) AS AverageSales, SUM(sales_amount) AS TotalSales
FROM sales
GROUP BY product_category
HAVING SUM(sales_amount) > 50000
ORDER BY AverageSales DESC;
```

This query groups the sales data by `product_category`, calculates the average and total sales amount for each category, filters out categories with total sales of 50,000 or less, and orders the result by average sales in descending order.

The `HAVING` clause is a powerful tool for filtering groups of data in SQL, allowing you to perform more detailed and specific data analysis.


### `EXISTS` operator

The `EXISTS` operator in SQL is used to check the presence of rows in a subquery. It returns `TRUE` if the subquery returns one or more records, and `FALSE` otherwise. The `EXISTS` operator is commonly used to perform conditional checks within queries, often to determine if certain related records exist in another table.

### Syntax

```sql
SELECT column_name(s)
FROM table_name
WHERE EXISTS (subquery);
```

### Examples

#### 1. Basic Usage

To find employees who belong to a department:

```sql
SELECT employee_id, first_name, last_name
FROM employees e
WHERE EXISTS (
    SELECT 1
    FROM departments d
    WHERE e.department_id = d.department_id
);
```

This query retrieves employees who have a corresponding department in the `departments` table.

#### 2. Using `EXISTS` with Subqueries

To find customers who have placed orders:

```sql
SELECT customer_id, customer_name
FROM customers c
WHERE EXISTS (
    SELECT 1
    FROM orders o
    WHERE c.customer_id = o.customer_id
);
```

This query retrieves customers who have at least one order in the `orders` table.

#### 3. Using `NOT EXISTS`

To find employees who do not belong to any department:

```sql
SELECT employee_id, first_name, last_name
FROM employees e
WHERE NOT EXISTS (
    SELECT 1
    FROM departments d
    WHERE e.department_id = d.department_id
);
```

This query retrieves employees who do not have a corresponding department in the `departments` table.

### Example Scenarios

#### 1. Filtering with Conditions

To find products that have never been sold:

```sql
SELECT product_id, product_name
FROM products p
WHERE NOT EXISTS (
    SELECT 1
    FROM sales s
    WHERE p.product_id = s.product_id
);
```

#### 2. Combining `EXISTS` with `JOIN`

To find employees who have a manager in the same department:

```sql
SELECT e1.employee_id, e1.first_name, e1.last_name
FROM employees e1
WHERE EXISTS (
    SELECT 1
    FROM employees e2
    WHERE e1.manager_id = e2.employee_id
    AND e1.department_id = e2.department_id
);
```

#### 3. Using `EXISTS` in Update Statements

To give a salary raise to employees who have completed at least one project:

```sql
UPDATE employees e
SET salary = salary * 1.1
WHERE EXISTS (
    SELECT 1
    FROM projects p
    WHERE e.employee_id = p.employee_id
);
```

#### 4. Using `EXISTS` with Aggregation

To find departments with more than 10 employees:

```sql
SELECT department_id, department_name
FROM departments d
WHERE EXISTS (
    SELECT 1
    FROM employees e
    WHERE e.department_id = d.department_id
    GROUP BY e.department_id
    HAVING COUNT(e.employee_id) > 10
);
```

### Important Points

- **Performance**: The `EXISTS` operator can be more efficient than `IN` for subqueries with large result sets because `EXISTS` can short-circuit once a match is found.
- **Return Value**: The subquery within `EXISTS` usually returns `1` or `NULL`, but the actual returned value is irrelevant. The existence of any row is what determines the `TRUE` or `FALSE` result.
- **Use Case**: `EXISTS` is typically used when checking for the existence of rows that meet certain conditions in a related table.

### Complex Example

To find employees who have been assigned to at least one project and have a salary greater than 60,000:

```sql
SELECT employee_id, first_name, last_name, salary
FROM employees e
WHERE EXISTS (
    SELECT 1
    FROM projects p
    WHERE e.employee_id = p.employee_id
)
AND salary > 60000;
```

This query first checks if an employee is assigned to any project using the `EXISTS` operator and then filters the results to include only those employees with a salary greater than 60,000.

The `EXISTS` operator is a powerful tool for checking the existence of records in a subquery, allowing for efficient and flexible data retrieval based on complex conditions.


### `ANY` and `ALL` operators
In SQL, the `ANY` and `ALL` operators are used with subqueries to compare a value to a set of values returned by the subquery.

### The `ANY` Operator

The `ANY` operator returns `TRUE` if any of the subquery values satisfy the condition. It allows a comparison to a range of values and can be used with various comparison operators such as `=`, `>`, `<`, `>=`, `<=`, and `<>`.

#### Syntax

```sql
SELECT column_name(s)
FROM table_name
WHERE column_name comparison_operator ANY (subquery);
```

#### Example

To find employees who earn more than the salary of at least one employee in department 10:

```sql
SELECT employee_id, first_name, salary
FROM employees
WHERE salary > ANY (
    SELECT salary
    FROM employees
    WHERE department_id = 10
);
```

### The `ALL` Operator

The `ALL` operator returns `TRUE` if all of the subquery values satisfy the condition. It also allows a comparison to a range of values but ensures that the condition is true for every value returned by the subquery.

#### Syntax

```sql
SELECT column_name(s)
FROM table_name
WHERE column_name comparison_operator ALL (subquery);
```

#### Example

To find employees who earn more than all employees in department 20:

```sql
SELECT employee_id, first_name, salary
FROM employees
WHERE salary > ALL (
    SELECT salary
    FROM employees
    WHERE department_id = 20
);
```

### Example Scenarios

#### 1. Using `ANY` with Different Comparison Operators

To find products with a price less than any product in category 5:

```sql
SELECT product_id, product_name, price
FROM products
WHERE price < ANY (
    SELECT price
    FROM products
    WHERE category_id = 5
);
```

#### 2. Combining `ANY` with Aggregates

To find employees who have made sales greater than the average sale amount of any employee:

```sql
SELECT employee_id, first_name, total_sales
FROM employees
WHERE total_sales > ANY (
    SELECT AVG(total_sales)
    FROM employees
    GROUP BY department_id
);
```

#### 3. Using `ALL` with Different Comparison Operators

To find products with a price greater than all products in category 3:

```sql
SELECT product_id, product_name, price
FROM products
WHERE price > ALL (
    SELECT price
    FROM products
    WHERE category_id = 3
);
```

#### 4. Combining `ALL` with Aggregates

To find employees whose salary is above the maximum salary in all other departments:

```sql
SELECT employee_id, first_name, salary
FROM employees e1
WHERE salary > ALL (
    SELECT MAX(salary)
    FROM employees e2
    WHERE e1.department_id <> e2.department_id
    GROUP BY department_id
);
```

### Important Points

- **Comparison with Subqueries**: `ANY` and `ALL` are typically used with subqueries to perform comparisons with a list of values.
- **Operators**: Can be used with various comparison operators to compare a column's value against multiple values returned by a subquery.
- **Efficiency**: The efficiency of queries using `ANY` and `ALL` can vary depending on the size and complexity of the subqueries. Proper indexing and query optimization techniques are recommended.

### Complex Example

To find employees who have a salary greater than the highest salary in any other department:

```sql
SELECT employee_id, first_name, salary
FROM employees e
WHERE salary > ANY (
    SELECT MAX(salary)
    FROM employees
    WHERE department_id <> e.department_id
    GROUP BY department_id
);
```

This query retrieves employees whose salary is greater than the highest salary of employees in any other department. It uses the `ANY` operator to compare the salary against the maximum salaries of all other departments.

By using `ANY` and `ALL` operators, you can perform more flexible and powerful comparisons in SQL, enabling complex data retrieval and analysis.


### `SELECT INTO` statement

The `SELECT INTO` statement in SQL is used to copy data from one table into a new table. The new table will be created with the same structure as the source table, including the data types of the columns. This statement is often used for creating backup copies of tables or for archiving data.

### Syntax

```sql
SELECT column1, column2, ...
INTO new_table
FROM existing_table
WHERE condition;
```

### Example Usage

1. **Copying All Data from a Table**

   To create a backup of the `employees` table:

   ```sql
   SELECT *
   INTO employees_backup
   FROM employees;
   ```

   This query creates a new table `employees_backup` with the same structure and data as the `employees` table.

2. **Copying Specific Columns**

   To copy only the `employee_id` and `first_name` columns from the `employees` table:

   ```sql
   SELECT employee_id, first_name
   INTO employees_backup
   FROM employees;
   ```

   This query creates a new table `employees_backup` with only the `employee_id` and `first_name` columns.

3. **Copying Data with a Condition**

   To copy only the employees who belong to department 10:

   ```sql
   SELECT employee_id, first_name, last_name
   INTO department_10_employees
   FROM employees
   WHERE department_id = 10;
   ```

   This query creates a new table `department_10_employees` containing only the employees from department 10.

4. **Copying Data with a Join**

   To create a new table that includes employee names and their corresponding department names:

   ```sql
   SELECT e.employee_id, e.first_name, e.last_name, d.department_name
   INTO employees_with_departments
   FROM employees e
   JOIN departments d ON e.department_id = d.department_id;
   ```

   This query creates a new table `employees_with_departments` containing employee details along with their department names.

### Important Points

- **Table Creation**: The `SELECT INTO` statement creates the new table automatically. If a table with the same name already exists, the query will fail.
- **Column Types**: The new table will have the same column data types as those in the original table.
- **Indexes and Constraints**: The new table will not inherit indexes, primary keys, or constraints from the original table. These need to be added separately if required.
- **Database Support**: The `SELECT INTO` statement is supported by many relational database management systems (RDBMS) like SQL Server and PostgreSQL, but not by some others like MySQL (which uses `CREATE TABLE ... AS SELECT` instead).

### Using `CREATE TABLE AS` in MySQL

MySQL does not support the `SELECT INTO` statement directly. Instead, you can use the `CREATE TABLE AS` statement.

```sql
CREATE TABLE new_table AS
SELECT column1, column2, ...
FROM existing_table
WHERE condition;
```

#### Example in MySQL

To create a backup of the `employees` table in MySQL:

```sql
CREATE TABLE employees_backup AS
SELECT *
FROM employees;
```

### Complex Example

To create a new table that includes the top 5 highest-paid employees along with their department names:

```sql
SELECT e.employee_id, e.first_name, e.last_name, e.salary, d.department_name
INTO top_5_highest_paid_employees
FROM employees e
JOIN departments d ON e.department_id = d.department_id
ORDER BY e.salary DESC
LIMIT 5;
```

This query creates a new table `top_5_highest_paid_employees` containing details of the top 5 highest-paid employees along with their department names.

### Conclusion

The `SELECT INTO` statement is a powerful tool for copying data into a new table with ease. Whether you are creating backups, archiving data, or generating summary tables, `SELECT INTO` provides a straightforward and efficient way to duplicate data.


### `INSERT INTO SELECT` statement

The `INSERT INTO SELECT` statement in SQL is used to copy data from one table and insert it into another existing table. This is particularly useful for transferring data between tables, copying data for backups, or populating tables with related data.

### Syntax

```sql
INSERT INTO target_table (column1, column2, ...)
SELECT column1, column2, ...
FROM source_table
WHERE condition;
```

### Example Usage

#### 1. Basic Example: Copying Data

To copy all data from `source_table` to `target_table`:

```sql
INSERT INTO target_table
SELECT *
FROM source_table;
```

#### 2. Copying Specific Columns

To copy only specific columns from `source_table` to `target_table`:

```sql
INSERT INTO target_table (column1, column2)
SELECT column1, column2
FROM source_table;
```

#### 3. Copying Data with a Condition

To copy only certain rows from `source_table` to `target_table` based on a condition:

```sql
INSERT INTO target_table (column1, column2)
SELECT column1, column2
FROM source_table
WHERE condition;
```

For example, to copy employees from `employees` table to `target_employees` table who belong to department 10:

```sql
INSERT INTO target_employees (employee_id, first_name, last_name)
SELECT employee_id, first_name, last_name
FROM employees
WHERE department_id = 10;
```

#### 4. Combining Data from Multiple Tables

To copy and combine data from multiple tables into `target_table` using a join:

```sql
INSERT INTO target_table (column1, column2, column3)
SELECT a.column1, b.column2, c.column3
FROM table1 a
JOIN table2 b ON a.common_field = b.common_field
JOIN table3 c ON b.other_common_field = c.other_common_field
WHERE condition;
```

### Example Scenarios

#### 1. Copying Data with Transformation

To insert data into `target_table` with some transformations applied:

```sql
INSERT INTO target_table (column1, column2, column3)
SELECT column1, column2, column3 * 1.1
FROM source_table;
```

#### 2. Inserting Data with Aggregation

To copy aggregated data from `source_table` to `target_table`:

```sql
INSERT INTO target_table (department_id, total_salary)
SELECT department_id, SUM(salary)
FROM source_table
GROUP BY department_id;
```

#### 3. Using Subqueries

To insert data based on the result of a subquery:

```sql
INSERT INTO target_table (column1, column2)
SELECT column1, column2
FROM source_table
WHERE column3 IN (SELECT column3 FROM another_table WHERE condition);
```

### Important Points

- **Table Structure**: The target table must already exist and have a structure compatible with the columns being inserted.
- **Column Count**: The number of columns in the `INSERT INTO` clause must match the number of columns in the `SELECT` clause.
- **Data Types**: The data types of the selected columns must be compatible with the data types of the columns in the target table.
- **Constraints and Indexes**: If the target table has constraints (e.g., primary keys, foreign keys) or indexes, ensure that the data being inserted complies with these constraints to avoid errors.

### Complex Example

To insert data from `employees` table into `high_earning_employees` table for employees who earn more than the average salary, along with the department name:

```sql
INSERT INTO high_earning_employees (employee_id, first_name, last_name, salary, department_name)
SELECT e.employee_id, e.first_name, e.last_name, e.salary, d.department_name
FROM employees e
JOIN departments d ON e.department_id = d.department_id
WHERE e.salary > (SELECT AVG(salary) FROM employees);
```

This query inserts data into `high_earning_employees` table, including only those employees whose salary is above the average salary, and it also includes the department name.

### Conclusion

The `INSERT INTO SELECT` statement is a powerful tool for copying and transforming data between tables. It allows you to efficiently transfer data while applying conditions, transformations, and aggregations as needed. This capability is essential for data migration, backup, and data warehousing tasks in database management.


### `CASE` expression

The `CASE` expression in SQL is a versatile conditional statement that allows you to return different values based on different conditions. It is similar to an `if-else` statement in programming languages and can be used in various parts of SQL queries, such as `SELECT`, `UPDATE`, `INSERT`, and `ORDER BY` clauses.

### Syntax

There are two forms of the `CASE` expression: the simple `CASE` expression and the searched `CASE` expression.

#### 1. Simple `CASE` Expression

The simple `CASE` expression compares an expression to a set of simple expressions to determine the result.

```sql
CASE expression
    WHEN value1 THEN result1
    WHEN value2 THEN result2
    ...
    ELSE resultN
END
```

#### 2. Searched `CASE` Expression

The searched `CASE` expression evaluates a set of Boolean expressions to determine the result.

```sql
CASE
    WHEN condition1 THEN result1
    WHEN condition2 THEN result2
    ...
    ELSE resultN
END
```

### Examples

#### 1. Simple `CASE` Expression

To assign a grade based on a numerical score:

```sql
SELECT student_id, 
       score,
       CASE score
           WHEN 100 THEN 'A+'
           WHEN 90 THEN 'A'
           WHEN 80 THEN 'B'
           WHEN 70 THEN 'C'
           ELSE 'F'
       END AS grade
FROM students;
```

#### 2. Searched `CASE` Expression

To categorize employees based on their salary:

```sql
SELECT employee_id, 
       salary,
       CASE 
           WHEN salary > 100000 THEN 'High'
           WHEN salary BETWEEN 50000 AND 100000 THEN 'Medium'
           ELSE 'Low'
       END AS salary_category
FROM employees;
```

#### 3. Using `CASE` in `ORDER BY`

To sort products based on their availability and price:

```sql
SELECT product_id, product_name, stock_quantity, price
FROM products
ORDER BY 
    CASE 
        WHEN stock_quantity = 0 THEN 1
        ELSE 0
    END,
    price DESC;
```

This query sorts products, placing out-of-stock items at the end, and then sorts by price in descending order.

#### 4. Using `CASE` in `UPDATE`

To give a salary raise based on the current salary:

```sql
UPDATE employees
SET salary = 
    CASE 
        WHEN salary < 50000 THEN salary * 1.10
        WHEN salary BETWEEN 50000 AND 100000 THEN salary * 1.05
        ELSE salary * 1.02
    END;
```

#### 5. Using `CASE` in `WHERE`

To filter records based on conditional logic:

```sql
SELECT employee_id, first_name, last_name, department_id
FROM employees
WHERE 
    CASE 
        WHEN department_id = 10 THEN 1
        WHEN department_id = 20 THEN 1
        ELSE 0
    END = 1;
```

### Complex Example

To create a report categorizing employees' performance based on their sales and rating:

```sql
SELECT employee_id, first_name, last_name, sales, rating,
       CASE 
           WHEN sales > 100000 AND rating = 'Excellent' THEN 'Outstanding'
           WHEN sales > 75000 AND rating IN ('Excellent', 'Good') THEN 'Very Good'
           WHEN sales > 50000 THEN 'Good'
           ELSE 'Needs Improvement'
       END AS performance_category
FROM employees;
```

This query categorizes employees into different performance categories based on their sales and ratings.

### Important Points

- **NULL Handling**: The `CASE` expression can handle `NULL` values, and specific conditions can be included to deal with `NULL`s.
- **Data Type Consistency**: All result expressions in the `CASE` statement should return the same data type.
- **Execution Flow**: The `CASE` expression stops evaluating conditions once it finds the first condition that is `TRUE`.

The `CASE` expression is a powerful tool in SQL for implementing complex conditional logic within your queries. It enhances the flexibility and readability of SQL statements, enabling sophisticated data manipulation and analysis.



### `CASE` Expression

The `CASE` expression in SQL is a versatile conditional statement that allows you to return different values based on different conditions. It is similar to an `if-else` statement in programming languages and can be used in various parts of SQL queries, such as `SELECT`, `UPDATE`, `INSERT`, and `ORDER BY` clauses.

### Syntax

There are two forms of the `CASE` expression: the simple `CASE` expression and the searched `CASE` expression.

#### 1. Simple `CASE` Expression

The simple `CASE` expression compares an expression to a set of simple expressions to determine the result.

```sql
CASE expression
    WHEN value1 THEN result1
    WHEN value2 THEN result2
    ...
    ELSE resultN
END
```

#### 2. Searched `CASE` Expression

The searched `CASE` expression evaluates a set of Boolean expressions to determine the result.

```sql
CASE
    WHEN condition1 THEN result1
    WHEN condition2 THEN result2
    ...
    ELSE resultN
END
```

### Examples

#### 1. Simple `CASE` Expression

To assign a grade based on a numerical score:

```sql
SELECT student_id, 
       score,
       CASE score
           WHEN 100 THEN 'A+'
           WHEN 90 THEN 'A'
           WHEN 80 THEN 'B'
           WHEN 70 THEN 'C'
           ELSE 'F'
       END AS grade
FROM students;
```

#### 2. Searched `CASE` Expression

To categorize employees based on their salary:

```sql
SELECT employee_id, 
       salary,
       CASE 
           WHEN salary > 100000 THEN 'High'
           WHEN salary BETWEEN 50000 AND 100000 THEN 'Medium'
           ELSE 'Low'
       END AS salary_category
FROM employees;
```

#### 3. Using `CASE` in `ORDER BY`

To sort products based on their availability and price:

```sql
SELECT product_id, product_name, stock_quantity, price
FROM products
ORDER BY 
    CASE 
        WHEN stock_quantity = 0 THEN 1
        ELSE 0
    END,
    price DESC;
```

This query sorts products, placing out-of-stock items at the end, and then sorts by price in descending order.

#### 4. Using `CASE` in `UPDATE`

To give a salary raise based on the current salary:

```sql
UPDATE employees
SET salary = 
    CASE 
        WHEN salary < 50000 THEN salary * 1.10
        WHEN salary BETWEEN 50000 AND 100000 THEN salary * 1.05
        ELSE salary * 1.02
    END;
```

#### 5. Using `CASE` in `WHERE`

To filter records based on conditional logic:

```sql
SELECT employee_id, first_name, last_name, department_id
FROM employees
WHERE 
    CASE 
        WHEN department_id = 10 THEN 1
        WHEN department_id = 20 THEN 1
        ELSE 0
    END = 1;
```

### Complex Example

To create a report categorizing employees' performance based on their sales and rating:

```sql
SELECT employee_id, first_name, last_name, sales, rating,
       CASE 
           WHEN sales > 100000 AND rating = 'Excellent' THEN 'Outstanding'
           WHEN sales > 75000 AND rating IN ('Excellent', 'Good') THEN 'Very Good'
           WHEN sales > 50000 THEN 'Good'
           ELSE 'Needs Improvement'
       END AS performance_category
FROM employees;
```

This query categorizes employees into different performance categories based on their sales and ratings.

### Important Points

- **NULL Handling**: The `CASE` expression can handle `NULL` values, and specific conditions can be included to deal with `NULL`s.
- **Data Type Consistency**: All result expressions in the `CASE` statement should return the same data type.
- **Execution Flow**: The `CASE` expression stops evaluating conditions once it finds the first condition that is `TRUE`.

The `CASE` expression is a powerful tool in SQL for implementing complex conditional logic within your queries. It enhances the flexibility and readability of SQL statements, enabling sophisticated data manipulation and analysis.



### What is a Stored Procedure?
A stored procedure is a prepared SQL code that you can save, so the code can be reused over and over again.

So if you have an SQL query that you write over and over again, save it as a stored procedure, and then just call it to execute it.

You can also pass parameters to a stored procedure, so that the stored procedure can act based on the parameter value(s) that is passed.

(A stored procedure is a precompiled collection of SQL statements and optional control-of-flow statements, stored under a name and processed as a unit. Stored procedures allow for modular, reusable code and can improve performance because the SQL statements are precompiled. They can accept input parameters, output parameters, and return multiple result sets.)

### Benefits of Stored Procedures

1. **Performance**: Since stored procedures are precompiled, they often run faster than dynamic SQL.
2. **Modularity**: They allow for modular programming, where different procedures can be developed and tested independently.
3. **Security**: They can help enforce security policies by controlling user access to the underlying data.
4. **Maintainability**: Changes to business logic can be made in one place and affect all applications that use the stored procedure.

### Syntax

#### Creating a Stored Procedure

**SQL Server:**

```sql
CREATE PROCEDURE procedure_name
    @parameter1 datatype,
    @parameter2 datatype OUTPUT,
    ...
AS
BEGIN
    -- SQL statements
END;
```

**MySQL:**

```sql
CREATE PROCEDURE procedure_name(IN parameter1 datatype, OUT parameter2 datatype, ...)
BEGIN
    -- SQL statements
END;
```

**Oracle:**

```sql
CREATE PROCEDURE procedure_name (
    parameter1 IN datatype,
    parameter2 OUT datatype,
    ...
) AS
BEGIN
    -- SQL statements
END;
```

### Examples

#### 1. Simple Stored Procedure

To create a stored procedure that retrieves all employees from a specific department:

**SQL Server:**

```sql
CREATE PROCEDURE GetEmployeesByDepartment
    @DepartmentId INT
AS
BEGIN
    SELECT EmployeeId, FirstName, LastName, DepartmentId
    FROM Employees
    WHERE DepartmentId = @DepartmentId;
END;
```

**MySQL:**

```sql
DELIMITER //

CREATE PROCEDURE GetEmployeesByDepartment(IN DepartmentId INT)
BEGIN
    SELECT EmployeeId, FirstName, LastName, DepartmentId
    FROM Employees
    WHERE DepartmentId = DepartmentId;
END //

DELIMITER ;
```

#### 2. Stored Procedure with Output Parameter

To create a stored procedure that calculates the total sales for a specific employee and returns it:

**SQL Server:**

```sql
CREATE PROCEDURE GetTotalSales
    @EmployeeId INT,
    @TotalSales DECIMAL(10, 2) OUTPUT
AS
BEGIN
    SELECT @TotalSales = SUM(SalesAmount)
    FROM Sales
    WHERE EmployeeId = @EmployeeId;
END;
```

**MySQL:**

```sql
DELIMITER //

CREATE PROCEDURE GetTotalSales(IN EmployeeId INT, OUT TotalSales DECIMAL(10, 2))
BEGIN
    SELECT SUM(SalesAmount) INTO TotalSales
    FROM Sales
    WHERE EmployeeId = EmployeeId;
END //

DELIMITER ;
```

#### 3. Stored Procedure with Conditional Logic

To create a stored procedure that updates an employee's salary based on their performance rating:

**SQL Server:**

```sql
CREATE PROCEDURE UpdateSalaryBasedOnRating
    @EmployeeId INT,
    @Rating VARCHAR(10)
AS
BEGIN
    IF @Rating = 'Excellent'
    BEGIN
        UPDATE Employees
        SET Salary = Salary * 1.10
        WHERE EmployeeId = @EmployeeId;
    END
    ELSE IF @Rating = 'Good'
    BEGIN
        UPDATE Employees
        SET Salary = Salary * 1.05
        WHERE EmployeeId = @EmployeeId;
    END
    ELSE
    BEGIN
        UPDATE Employees
        SET Salary = Salary * 1.02
        WHERE EmployeeId = @EmployeeId;
    END
END;
```

**MySQL:**

```sql
DELIMITER //

CREATE PROCEDURE UpdateSalaryBasedOnRating(IN EmployeeId INT, IN Rating VARCHAR(10))
BEGIN
    IF Rating = 'Excellent' THEN
        UPDATE Employees
        SET Salary = Salary * 1.10
        WHERE EmployeeId = EmployeeId;
    ELSEIF Rating = 'Good' THEN
        UPDATE Employees
        SET Salary = Salary * 1.05
        WHERE EmployeeId = EmployeeId;
    ELSE
        UPDATE Employees
        SET Salary = Salary * 1.02
        WHERE EmployeeId = EmployeeId;
    END IF;
END //

DELIMITER ;
```

### Executing a Stored Procedure

#### SQL Server

To execute the stored procedure `GetEmployeesByDepartment`:

```sql
EXEC GetEmployeesByDepartment @DepartmentId = 1;
```

To execute the stored procedure `GetTotalSales` and get the output value:

```sql
DECLARE @TotalSales DECIMAL(10, 2);
EXEC GetTotalSales @EmployeeId = 1, @TotalSales = @TotalSales OUTPUT;
SELECT @TotalSales;
```

#### MySQL

To execute the stored procedure `GetEmployeesByDepartment`:

```sql
CALL GetEmployeesByDepartment(1);
```

To execute the stored procedure `GetTotalSales` and get the output value:

```sql
CALL GetTotalSales(1, @TotalSales);
SELECT @TotalSales;
```

### Important Points

- **Error Handling**: Implement error handling within your stored procedures to manage exceptions and unexpected conditions.
- **Transactions**: Use transactions within stored procedures to ensure data integrity.
- **Permissions**: Ensure that appropriate permissions are granted to users to execute stored procedures.
- **Optimization**: Optimize stored procedures to enhance performance, especially when dealing with large datasets or complex logic.

Stored procedures are a powerful feature in SQL that help encapsulate business logic, improve performance, and maintain data integrity. By using stored procedures, you can ensure that your database operations are efficient, secure, and manageable.

### SQL comments
In SQL, comments are used to add explanatory notes within the code. They are ignored by the database engine during query execution and are purely for human readability. Comments help improve the understanding of the code for developers, maintainers, and anyone else who may review it.

### Syntax

#### Single-Line Comments

In MySQL and PostgreSQL, single-line comments start with `--` or `#` and continue until the end of the line.

```sql
-- This is a single-line comment in MySQL
# This is also a single-line comment in MySQL

-- This is a single-line comment in PostgreSQL
```

#### Multi-Line Comments

MySQL and PostgreSQL support multi-line comments enclosed between `/*` and `*/`.

```sql
/* This is a
   multi-line comment */
```

### Example

```sql
-- This query selects all columns from the "employees" table
SELECT *
FROM employees
WHERE department_id = 10; -- Selects employees from department 10

/* 
This query calculates the total sales amount
for each employee and orders the results by
the total sales amount in descending order
*/
SELECT employee_id,
       SUM(sales_amount) AS total_sales
FROM sales
GROUP BY employee_id
ORDER BY total_sales DESC;
```

### Importance of Comments

1. **Code Documentation**: Comments provide context and explanation for the code, making it easier for others to understand its purpose and functionality.
2. **Code Maintenance**: Comments help developers understand the code they are working with, making it easier to update, modify, or debug.
3. **Collaboration**: Comments facilitate collaboration among team members by improving code comprehension and reducing ambiguity.
4. **Regulatory Compliance**: In regulated industries, comments may be required to document compliance with standards and regulations.

### Best Practices

1. **Be Clear and Concise**: Write comments that are informative but not overly verbose.
2. **Update Comments with Code**: Keep comments synchronized with the code they refer to, especially after making changes.
3. **Avoid Redundancy**: Don't duplicate information already evident in the code; focus on providing additional insights or clarifications.
4. **Use Standard Formats**: Follow established conventions for writing comments to maintain consistency across the codebase.

### Conclusion

Comments are an essential aspect of writing maintainable and understandable SQL code. By incorporating comments effectively, you can improve code quality, facilitate collaboration, and ensure that your SQL queries are comprehensible to others.


SQL operators are symbols or keywords used in SQL statements to perform operations such as arithmetic operations, comparison operations, logical operations, and string operations. Here are some common SQL operators:

### Arithmetic Operators

1. **Addition (+)**: Adds two values.
2. **Subtraction (-)**: Subtracts one value from another.
3. **Multiplication (*)**: Multiplies two values.
4. **Division (/)**: Divides one value by another.
5. **Modulus (%)**: Returns the remainder of a division.

### Comparison Operators

1. **Equal to (=)**: Compares if two values are equal.
2. **Not equal to (<>, !=)**: Compares if two values are not equal.
3. **Greater than (>)**: Compares if one value is greater than another.
4. **Less than (<)**: Compares if one value is less than another.
5. **Greater than or equal to (>=)**: Compares if one value is greater than or equal to another.
6. **Less than or equal to (<=)**: Compares if one value is less than or equal to another.
7. **LIKE**: Compares a value to a pattern using wildcard characters.
8. **BETWEEN**: Checks if a value is within a range of values.
9. **IN**: Checks if a value matches any value in a list.

### Logical Operators

1. **AND**: Returns true if all conditions are true.
2. **OR**: Returns true if any condition is true.
3. **NOT**: Negates a condition.

### String Operators

1. **Concatenation (||)**: Concatenates two strings.
2. **LIKE**: Compares a value to a pattern using wildcard characters.

### Other Operators

1. **IS NULL**: Checks if a value is NULL.
2. **IS NOT NULL**: Checks if a value is not NULL.

### Example Usage

```sql
-- Arithmetic operators
SELECT 10 + 5; -- Returns 15
SELECT 10 - 5; -- Returns 5
SELECT 10 * 5; -- Returns 50
SELECT 10 / 5; -- Returns 2
SELECT 10 % 3; -- Returns 1

-- Comparison operators
SELECT * FROM employees WHERE salary > 50000;
SELECT * FROM products WHERE category_id <> 2;
SELECT * FROM orders WHERE order_date >= '2022-01-01';

-- Logical operators
SELECT * FROM customers WHERE city = 'New York' AND age > 30;
SELECT * FROM products WHERE price < 100 OR stock_quantity > 0;
SELECT * FROM employees WHERE NOT department_id = 10;

-- String operators
SELECT first_name || ' ' || last_name AS full_name FROM employees;
SELECT * FROM products WHERE product_name LIKE '%apple%';

-- Other operators
SELECT * FROM employees WHERE commission IS NULL;
SELECT * FROM employees WHERE department_id IN (1, 2, 3);
```

These operators are fundamental to constructing SQL queries for data retrieval, manipulation, and analysis. Understanding their usage is crucial for effective SQL programming.