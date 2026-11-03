Introduction to SQL: A Beginner's Guide to Creating, Reading, Updating, and Deleting Data

Intoduction

Have you ever wondered how applications store user information, how banks manage customer records, or how online stores keep track of products, prices, and orders?

Behind many of these systems is a database, and one of the most widely used languages for working with relational databases is **SQL (Structured Query Language)**.

I recently completed a short course on Introduction to SQL, where I learned fundamental SQL queries for creating tables, retrieving information, inserting records, modifying existing data, deleting records, and applying constraints.

As part of my learning journey in technology, I want to share these fundamentals in a simple, practical way for anyone taking their first steps into databases, data analysis, software development, or cloud computing.

Let's get started!

## 1. What is SQL?

SQL stands for **Structured Query Language**. It is a language used to communicate with relational database management systems (RDBMS) such as:

- MySQL
- PostgreSQL
- Microsoft SQL Server
- SQLite
- Oracle Database

SQL allows us to create database structures, store information, retrieve records, update data, and manage how information is organized.

For example, imagine a school database containing students' names, ages, and identification numbers. Instead of keeping this information in separate documents, we can organize it in a database table and use SQL to manage it efficiently.

## 2. Why is SQL useful?

SQL is an important skill across several areas of technology and business.

**Data analysis:** Analysts use SQL to retrieve, filter, and organize data to discover trends and generate reports.

**Software development:** Developers use SQL to store and retrieve application data, such as customer accounts, orders, and transactions.

**Cloud computing:** Cloud engineers work with managed database services such as Azure SQL Database, Amazon RDS, and Google Cloud SQL.

**Business operations:** Organizations use databases to manage employees, inventory, customer records, and financial information.

**Data management:** SQL makes it possible to maintain structured information, enforce data rules, and modify records without manually editing every entry.

Learning SQL provides a foundation for understanding how modern applications and data-driven systems work.

## 3. Understanding database tables

A relational database organizes data into tables. A table contains **columns** and **rows**.

For example, a table called `students` could contain the following information:

| id | name | age |
|---:|---|---:|
| 1 | Ada | 22 |
| 2 | Chidi | 25 |
| 3 | Amaka | 20 |

Here:

- `id`, `name`, and `age` are columns.
- Each student's information represents a row.
- `INTEGER` is a data type used for whole numbers.
- `TEXT` is a data type used for text values.

Now let's explore the SQL commands used to create and manage a table like this.

## 4. Creating a table with CREATE TABLE

The `CREATE TABLE` statement creates a new table in a database.

```sql
CREATE TABLE students (
    id INTEGER,
    name TEXT,
    age INTEGER
);
```

Let's break it down:

- `CREATE TABLE` tells the database to create a new table.
- `students` is the table name.
- `id INTEGER` creates a column for whole numbers.
- `name TEXT` creates a column for text.
- `age INTEGER` creates a column for whole numbers.
- The parentheses contain the column definitions.

The semicolon (`;`) marks the end of the SQL statement.

**Why is this useful?**

Before storing information, we need a structure that defines how the data will be organized. Creating a table establishes that structure.

## 5. Retrieving data with SELECT

Once information has been stored in a table, we can retrieve it using `SELECT`.

To display all columns and rows from the students table, we write:

```sql
SELECT * FROM students;
```

The asterisk (`*`) means all columns.

If we only want students' names, we can specify the column:

```sql
SELECT name FROM students;
```

To retrieve both names and ages:

```sql
SELECT name, age
FROM students;
```

We can also filter results using `WHERE`:

```sql
SELECT *
FROM students
WHERE age = 22;
```

This returns only records where the student's age is 22.

**Why is this useful?**

The `SELECT` statement is essential when searching databases for specific information. For example, a business could retrieve customer details, find products, or generate reports from stored records.

## 6. Adding records with INSERT INTO

The `INSERT INTO` statement adds new records to a table.

For example:

```sql
INSERT INTO students (id, name, age)
VALUES (1, 'Ada', 22);
```

Here:

- `INSERT INTO students` identifies the table.
- `(id, name, age)` specifies the columns receiving data.
- `VALUES` provides the information to insert.
- `'Ada'` is enclosed in single quotes because it is text.

We can add another student:

```sql
INSERT INTO students (id, name, age)
VALUES (2, 'Chidi', 25);
```

Each statement inserts one new record.

**Why is this useful?**

Applications use insert operations whenever new information needs to be saved, such as registering a user, recording an order, or adding a new employee.

Note: These examples assume the table is empty. If an existing record already uses the same ID, the insert may fail when a uniqueness constraint is enforced.

## 7. Modifying a table with ALTER TABLE and ADD COLUMN

Sometimes, our database needs additional information that was not included when the table was first created.

For example, we may decide to store students' email addresses.

We can add a new column using:

```sql
ALTER TABLE students
ADD COLUMN email TEXT;
```

Let's understand the statement:

- `ALTER TABLE` modifies an existing table's structure.
- `students` identifies the table.
- `ADD COLUMN` adds a new column.
- `email TEXT` defines the new column and its data type.

Existing records will generally have `NULL` in the new column until a value is provided, depending on the database and column definition.

**Why is this useful?**

Database requirements change as applications grow. `ALTER TABLE` allows us to extend a table's structure without recreating the entire table.

The exact syntax and supported alterations can vary between database systems.

## 8. Updating existing records with UPDATE, SET, and WHERE

The `UPDATE` statement changes data already stored in a table.

Suppose Ada's age changes from 22 to 23. We can update her record with:

```sql
UPDATE students
SET age = 23
WHERE id = 1;
```

Let's break it down:

- `UPDATE students` identifies the table to modify.
- `SET age = 23` assigns a new value to the age column.
- `WHERE id = 1` identifies the record to update.

The `WHERE` clause is particularly important because it helps target the correct record.

**What happens if we leave out WHERE?**

```sql
UPDATE students
SET age = 23;
```

This statement can update the age of every row in the table.

Always check your conditions before running an update, especially in a production database.

**Why is this useful?**

Businesses frequently update customer information, employee details, product prices, and order statuses. The `UPDATE` statement makes these changes possible.

## 9. Deleting records with DELETE FROM

The `DELETE FROM` statement removes records from a table.

For example, to delete the student whose ID is 2:

```sql
DELETE FROM students
WHERE id = 2;
```

Here, `DELETE FROM students` identifies the table, while `WHERE id = 2` identifies the record to remove.

**Important:** Omitting the `WHERE` clause can delete every row in the table.

```sql
DELETE FROM students;
```

This removes all records but ordinarily leaves the table itself in place.

To remove the table structure entirely, a different command, `DROP TABLE`, is used.

**Why is this useful?**

Deleting data helps maintain accurate records, remove obsolete information, and support data-retention policies. In real applications, deletion should be handled carefully because it may be difficult to recover deleted records without backups or transaction support.

## 10. Understanding SQL constraints

Constraints are rules applied to table columns to help maintain accurate and reliable data.

Without constraints, a database might allow missing names, duplicate identifiers, or values that do not meet the requirements of the application.

Here are some common SQL constraints.

### PRIMARY KEY

A primary key uniquely identifies each record in a table.

```sql
CREATE TABLE students (
    id INTEGER PRIMARY KEY,
    name TEXT,
    age INTEGER
);
```

Each student must have a unique ID. A primary key cannot contain duplicate values or `NULL`.

### NOT NULL

The `NOT NULL` constraint prevents a column from accepting `NULL` values.

```sql
CREATE TABLE students (
    id INTEGER PRIMARY KEY,
    name TEXT NOT NULL,
    age INTEGER
);
```

This requires every inserted student record to include a non-`NULL` name.

### UNIQUE

The `UNIQUE` constraint prevents duplicate values in a column or combination of columns.

```sql
CREATE TABLE students (
    id INTEGER PRIMARY KEY,
    email TEXT UNIQUE
);
```

This helps prevent multiple records from sharing the same non-`NULL` email address. How `NULL` values are handled by unique constraints can vary by database system.

### CHECK

The `CHECK` constraint enforces a condition on the data.

```sql
CREATE TABLE students (
    id INTEGER PRIMARY KEY,
    name TEXT NOT NULL,
    age INTEGER CHECK (age >= 0)
);
```

This prevents the database from accepting a negative age when the constraint is enforced.

### DEFAULT

The `DEFAULT` constraint supplies a value when an insert does not specify one.

```sql
CREATE TABLE students (
    id INTEGER PRIMARY KEY,
    name TEXT NOT NULL,
    status TEXT DEFAULT 'active'
);
```

If a record is inserted without specifying `status`, the database uses `'active'`.

**Why are constraints useful?**

Constraints help enforce data integrity at the database level. They reduce the risk of invalid or inconsistent records and support more reliable applications.

## 11. Putting the commands together

Let's combine what we have learned into a simple workflow.

```sql
-- 1. Create the table
CREATE TABLE students (
    id INTEGER PRIMARY KEY,
    name TEXT NOT NULL,
    age INTEGER CHECK (age >= 0)
);

-- 2. Insert a record
INSERT INTO students (id, name, age)
VALUES (1, 'Ada', 22);

-- 3. Retrieve all records
SELECT * FROM students;

-- 4. Update a record
UPDATE students
SET age = 23
WHERE id = 1;

-- 5. Retrieve a specific record
SELECT *
FROM students
WHERE id = 1;

-- 6. Delete a record
DELETE FROM students
WHERE id = 1;
```

This example demonstrates a basic database lifecycle: creating a table, inserting information, reading it, updating it, and deleting it.

The comments beginning with `--` are explanatory notes and are not executed as SQL statements.

## 12. Best practices when learning SQL

As you continue practising SQL, keep these principles in mind:

1. **Use meaningful names.** Choose clear table and column names that describe the data they contain.
2. **Understand your data types.** Select appropriate types for numbers, text, dates, and other values.
3. **Use constraints.** Define rules that prevent invalid or duplicate data where appropriate.
4. **Be careful with UPDATE and DELETE.** Verify your `WHERE` conditions before executing changes.
5. **Practise with sample data.** Experiment in a local database before working with important information.
6. **Learn transactions and backups.** These concepts help protect data when changes go wrong.
7. **Keep learning.** Explore filtering, sorting, aggregate functions, joins, indexes, and database security as your confidence grows.

## Conclusion

Learning SQL has introduced me to an important part of how information is stored, organized, and managed in modern technology.

Understanding commands such as `CREATE TABLE`, `SELECT`, `INSERT INTO`, `ALTER TABLE`, `UPDATE`, and `DELETE FROM` provides a practical foundation for working with relational databases. Learning constraints also shows why data quality and integrity matter.

For anyone interested in data analysis, software development, cloud computing, or DevOps, SQL is a valuable skill to develop. Databases are a fundamental part of many applications, and knowing how to interact with them helps us better understand the systems we build and support.

This is another step in my journey of learning, practising, and sharing knowledge as I grow in technology.

**My next step:** Continue practising SQL and explore more advanced concepts, including filtering with `ORDER BY`, summarizing data with aggregate functions, and combining tables using `JOIN`.

If you are also learning SQL, I would love to hear from you in the comments:

**Which SQL command did you find easiest to understand, and which one took you the longest to learn?**

Let's keep learning and growing together!

 #SoftwareDevelopment #LearningInPublic