---
layout: post
title:  "Unit 3 Blog"
date:   2025-03-25 18:30:25
categories: Blog
tags: featured
image: /assets/article_images/2014-11-30-mediator_features/night-track.JPG
image2: /assets/article_images/2014-11-30-mediator_features/night-track-mobile.JPG


---

# A Comprehensive Guide to Database Systems Fundamentals: ACID Properties, SQL, and Advanced Querying

## Introduction

Database systems form the backbone of modern applications, storing and managing the data that powers everything from social networks to banking systems. In this comprehensive guide, we'll explore the fundamental concepts covered in the Database Systems Fundamentals course from the Royal University of Bhutan's College of Science and Technology. We'll delve into ACID properties, SQL fundamentals, transaction management, and advanced querying techniques that every database professional should master.

## Understanding Transactions and ACID Properties

### What is a Transaction?

In database systems, a **transaction** represents a single logical unit of work that accesses and possibly modifies the contents of a database. Transactions are crucial because they ensure data integrity when multiple operations need to be executed as an atomic unit.

For example, when transferring money between bank accounts, the transaction would involve:
1. Deducting the amount from the sender's account
2. Adding the amount to the receiver's account

Both operations must succeed or fail together to maintain account balance integrity.

### The ACID Properties

ACID is an acronym that stands for four key properties that guarantee reliable transaction processing:

1. **Atomicity (A)**
   - The entire transaction takes place at once or doesn't happen at all
   - There's no such thing as a "half-completed" transaction
   - If any part fails, the entire transaction is rolled back

2. **Consistency (C)**
   - The database must be consistent before and after the transaction
   - All data rules and constraints are maintained
   - Transactions bring the database from one valid state to another

3. **Isolation (I)**
   - Multiple transactions occur independently without interference
   - Concurrent transactions don't affect each other
   - Intermediate transaction states are invisible to other transactions

4. **Durability (D)**
   - Changes of a successful transaction persist even if system failure occurs
   - Once committed, changes are permanent
   - Typically implemented through transaction logs

These properties work together to ensure data reliability in multi-user database environments.

## SQL Fundamentals

### History of SQL

SQL (Structured Query Language) has a rich history:
- Originally called "Sequel"
- Developed by IBM as part of the System R project in the 1970s
- Became a standard language for relational database management systems (RDBMS)
- Now governed by ISO/IEC standards with various implementations (MySQL, PostgreSQL, SQL Server, Oracle, etc.)

### SQL Components

SQL consists of several key parts:

1. **Data Definition Language (DDL)**
   - Used to define and modify database structure
   - Commands: CREATE, ALTER, DROP, TRUNCATE, RENAME

2. **Data Manipulation Language (DML)**
   - Used to manipulate data within database objects
   - Commands: SELECT, INSERT, UPDATE, DELETE

3. **Data Control Language (DCL)**
   - Used to control access to data
   - Commands: GRANT, REVOKE


### Basic SQL Data Types

SQL supports various data types to store different kinds of information:

- **Character Types**:
  - `CHAR(n)`: Fixed-length character string (e.g., `CHAR(10) 'Hello'`)
  - `VARCHAR(n)`: Variable-length string up to n characters (e.g., `VARCHAR(20) 'Hello world'`)

- **Numeric Types**:
  - `INT`: Integer value (e.g., `25`)
  - `SMALLINT`: Smaller integer value (e.g., `10`)
  - `NUMERIC(p,s)`: Fixed-point number with p digits total, s after decimal (e.g., `NUMERIC(4,2) 10.50`)
  - `REAL`: Floating-point number (e.g., `25.35`)
  - `DOUBLE PRECISION`: High-precision floating point (e.g., `3.1415927`)
  - `FLOAT(n)`: Floating point with at least n digits precision (e.g., `FLOAT(5) 25.353`)

- **Date/Time Types**:
  - `DATE`: Calendar date (year, month, day)
  - `TIME`: Time of day (hours, minutes, seconds)
  - `TIMESTAMP`: Date and time combination

### SQL Constraints

Constraints enforce rules on data columns to ensure data integrity:

- **NOT NULL**: Ensures a column cannot have NULL values
- **UNIQUE**: Ensures all values in a column are different
- **PRIMARY KEY**: Combination of NOT NULL and UNIQUE, uniquely identifies each row
- **FOREIGN KEY**: Maintains referential integrity between tables
- **CHECK**: Ensures values satisfy a specific condition
- **DEFAULT**: Sets a default value when none is specified
- **CREATE INDEX**: Improves data retrieval speed

Example of constraints in table creation:
```sql
CREATE TABLE Users (
    Username varchar(255) PRIMARY KEY,
    DOB date NOT NULL,
    F_Name varchar(255),
    Gender varchar(10) CHECK (Gender IN ('Male', 'Female', 'Other'))
);
```

## Database Schema Definition

### Creating Databases and Tables

Basic database operations include:

1. **Creating a Database**:
   ```sql
   CREATE DATABASE AirlineTicketingDB;
   ```

2. **Listing Databases**:
   ```sql
   \l  
   ```

3. **Using a Database**:
   ```sql
   \c airlineticketingdb;  
   ```

4. **Creating Tables**:
   ```sql
   CREATE TABLE Flight (
       Flight_no varchar(10) PRIMARY KEY,
       Dep_time timestamp,
       Destination varchar(255),
       Source varchar(255),
       Arr_time timestamp,
       Distance int,
       Username varchar(255),
       FOREIGN KEY (Username) REFERENCES Users(Username)
   );
   ```

### Modifying Table Structure

The `ALTER TABLE` command allows modifying existing tables:

1. **Adding a Column**:
   ```sql
   ALTER TABLE Users ADD COLUMN Email varchar(255);
   ```

2. **Modifying a Column**:
   ```sql
   ALTER TABLE Users ALTER COLUMN DOB TYPE timestamp;
   ```

3. **Renaming a Table**:
   ```sql
   ALTER TABLE Users RENAME TO Customers;
   ```

4. **Renaming a Column**:
   ```sql
   ALTER TABLE Customers RENAME COLUMN F_Name TO First_Name;
   ```

### Deleting Database Objects

1. **Deleting Tables**:
   ```sql
   DROP TABLE User_Cancellation;
   ```

2. **Deleting Databases**:
   ```sql
   DROP DATABASE airlineticketingdb;
   ```

## Basic SQL Queries

### SELECT Statement Fundamentals

The SELECT statement retrieves data from one or more tables:

1. **Selecting All Columns**:
   ```sql
   SELECT * FROM Users;
   ```

2. **Selecting Specific Columns**:
   ```sql
   SELECT Username, F_Name, L_Name FROM Users;
   ```

3. **Filtering with WHERE Clause**:
   ```sql
   SELECT * FROM Users WHERE Gender = 'Male';
   ```

### Advanced Filtering

1. **Combining Conditions with AND/OR**:
   ```sql
   SELECT * FROM Users 
   WHERE Gender = 'Male' AND DOB > '1990-01-01';
   
   SELECT * FROM Users 
   WHERE Gender = 'Male' OR Gender = 'Female';
   ```

2. **Pattern Matching with LIKE**:
   ```sql
   -- Usernames starting with 'user'
   SELECT Username FROM Users WHERE Username LIKE 'user%';
   
   -- Usernames ending with '3'
   SELECT Username FROM Users WHERE Username LIKE '%3';
   
   -- Usernames containing 'ser' with exactly 5 characters
   SELECT Username FROM Users WHERE Username LIKE '__ser%';
   ```

3. **Sorting Results with ORDER BY**:
   ```sql
   SELECT * FROM Users 
   WHERE Gender = 'Male' 
   ORDER BY L_Name;
   
   SELECT * FROM Users 
   WHERE Gender = 'Male' 
   ORDER BY L_Name DESC;  -- Descending order
   ```

### Querying Multiple Tables

1. **Basic Join**:
   ```sql
   SELECT Ticket.PNR_No, Ticket.Flight_no, Users.F_Name
   FROM Ticket, Users
   WHERE Ticket.Booked_by_user = Users.Username;
   ```

2. **Using Table Aliases (AS)**:
   ```sql
   SELECT t.PNR_No, t.Flight_no, u.F_Name
   FROM Ticket AS t, Users AS u
   WHERE t.Booked_by_user = u.Username;
   ```

## Working with NULL Values

NULL represents missing or unknown data in SQL and requires special handling:

### NULL in Arithmetic Operations
- Any arithmetic operation with NULL yields NULL:
  ```sql
  SELECT 5 + NULL;  -- Result is NULL
  ```

### NULL in Comparisons
- Comparisons with NULL yield UNKNOWN (not true or false):
  ```sql
  SELECT * FROM Users WHERE Age > NULL;  -- Returns no rows
  ```

### Testing for NULL
- Use IS NULL or IS NOT NULL:
  ```sql
  SELECT * FROM Users WHERE Email IS NULL;
  SELECT * FROM Users WHERE Email IS NOT NULL;
  ```

### NULL in Logical Operations
- **AND**:
  - true AND unknown = unknown
  - false AND unknown = false
  - unknown AND unknown = unknown

- **OR**:
  - true OR unknown = true
  - false OR unknown = unknown
  - unknown OR unknown = unknown

- **NOT**:
  - NOT unknown = unknown

### NULL in Set Operations
- In UNION, INTERSECT, and EXCEPT operations:
  - NULLs are treated as identical to other NULLs
  - Different from comparison behavior where NULL = NULL is unknown

## Aggregation and Grouping

### Aggregate Functions

Aggregate functions perform calculations on sets of values:

1. **Basic Aggregates**:
   ```sql
   SELECT AVG(Fare) FROM Class;  -- Average fare
   SELECT MIN(Fare) FROM Class;  -- Minimum fare
   SELECT MAX(Fare) FROM Class;  -- Maximum fare
   SELECT COUNT(*) FROM Users;   -- Count of users
   ```

2. **GROUP BY Clause**:
   Groups rows sharing a property so aggregate functions can be applied:
   ```sql
   SELECT Class_type, AVG(Fare) 
   FROM Class 
   GROUP BY Class_type;
   ```

3. **HAVING Clause**:
   Filters groups after aggregation (WHERE filters before aggregation):
   ```sql
   SELECT Class_type, AVG(Fare) as avgFare
   FROM Class 
   GROUP BY Class_type
   HAVING AVG(Fare) > 300;
   ```

### Handling NULLs in Aggregation

- Aggregate functions ignore NULL values
- COUNT(*) counts all rows, COUNT(column) counts non-NULL values in column

## Advanced Query Techniques

### Nested Subqueries

Subqueries allow embedding queries within other queries:

1. **Subquery with IN**:
   ```sql
   SELECT * FROM Flight 
   WHERE Flight_no IN (
       SELECT Flight_no FROM Class 
       WHERE Class_type = 'Business'
   );
   ```

2. **Subquery with EXISTS**:
   ```sql
   SELECT * FROM Users u
   WHERE EXISTS (
       SELECT 1 FROM Ticket t 
       WHERE t.Booked_by_user = u.Username
   );
   ```

3. **Subquery in FROM Clause**:
   ```sql
   SELECT a.Airline_name, f.Destination
   FROM Airline a, 
       (SELECT * FROM Flight WHERE Distance > 1000) f
   WHERE a.Flight_no = f.Flight_no;
   ```

### Common Table Expressions (WITH Clause)

CTEs improve query readability and maintainability:
```sql
WITH HighValueTickets AS (
    SELECT * FROM Ticket 
    WHERE Class_id IN (
        SELECT Class_id FROM Class WHERE Fare > 300
    )
)
SELECT * FROM HighValueTickets;
```

### Set Operations

SQL supports standard set operations:

1. **UNION**: Combines results of two queries, removing duplicates
   ```sql
   SELECT Flight_no FROM Flight WHERE Source = 'New York'
   UNION
   SELECT Flight_no FROM Flight WHERE Destination = 'London';
   ```

2. **INTERSECT**: Returns only rows common to both queries
   ```sql
   SELECT Flight_no FROM Flight WHERE Distance > 1000
   INTERSECT
   SELECT Flight_no FROM Class WHERE Class_type = 'Business';
   ```

3. **EXCEPT**: Returns rows from first query not in second query
   ```sql
   SELECT Username FROM Users
   EXCEPT
   SELECT Booked_by_user FROM Ticket;
   ```

### Window Functions

Window functions perform calculations across related rows without grouping:

1. **Basic Window Function**:
   ```sql
   SELECT Flight_no, Fare,
          AVG(Fare) OVER (PARTITION BY Flight_no) as avgFare
   FROM Class;
   ```

2. **Ranking Functions**:
   ```sql
   SELECT Flight_no, Fare,
          ROW_NUMBER() OVER (ORDER BY Fare DESC) as rank
   FROM Class;
   ```

3. **Partitioned Ranking**:
   ```sql
   SELECT Flight_no, Class_type, Fare,
          RANK() OVER (PARTITION BY Flight_no ORDER BY Fare DESC) as classRank
   FROM Class;
   ```

## Database Modification

### Inserting Data

1. **Single Row Insert**:
   ```sql
   INSERT INTO Users (Username, F_Name, L_Name, Gender)
   VALUES ('user1', 'John', 'Doe', 'Male');
   ```

2. **Multiple Rows Insert**:
   ```sql
   INSERT INTO Users (Username, F_Name, L_Name, Gender)
   VALUES 
       ('user2', 'Jane', 'Smith', 'Female'),
       ('user3', 'Bob', 'Johnson', 'Male');
   ```

3. **Insert from Query**:
   ```sql
   INSERT INTO HighValueUsers (Username, Fare)
   SELECT u.Username, MAX(c.Fare)
   FROM Users u
   JOIN Ticket t ON u.Username = t.Booked_by_user
   JOIN Class c ON t.Class_id = c.Class_id
   GROUP BY u.Username
   HAVING MAX(c.Fare) > 500;
   ```

### Updating Data

1. **Simple Update**:
   ```sql
   UPDATE Class
   SET Fare = Fare * 1.1  -- 10% increase
   WHERE Class_type = 'Business';
   ```

2. **Conditional Update**:
   ```sql
   UPDATE Ticket
   SET Seat_no = 'A1'
   WHERE PNR_No = 'PNR123' AND Class_id = 1;
   ```

3. **Update with Subquery**:
   ```sql
   UPDATE Class
   SET Fare = Fare * 1.05
   WHERE Flight_no IN (
       SELECT Flight_no FROM Flight 
       WHERE Distance > 2000
   );
   ```

### Deleting Data

1. **Delete All Rows**:
   ```sql
   DELETE FROM User_Cancellation;  -- Careful!
   ```

2. **Conditional Delete**:
   ```sql
   DELETE FROM Ticket
   WHERE Date_time < '2023-01-01';
   ```

3. **Delete with Join**:
   ```sql
   DELETE FROM Ticket
   USING Users
   WHERE Ticket.Booked_by_user = Users.Username
   AND Users.Gender = 'Male';
   ```

## Conclusion

This comprehensive guide has covered the essential concepts of database systems, from the foundational ACID properties to advanced SQL querying techniques. We've explored:

1. The critical importance of transactions and how ACID properties ensure data integrity
2. SQL fundamentals including data types, constraints, and schema definition
3. Basic to advanced query techniques including joins, subqueries, and window functions
4. Handling special cases like NULL values and set operations
5. Database modification operations for inserting, updating, and deleting data

Mastering these concepts provides a solid foundation for working with relational database systems. Whether you're building simple applications or complex enterprise systems, understanding these database fundamentals is essential for creating efficient, reliable, and maintainable data storage solutions.


---




