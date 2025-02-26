---
layout: post
title:  "Reflections on Database Systems: A Journey Through Unit 1"
date:   2025-02-21 21:34:25
categories: Blog
tags: featured
image: /assets/article_images/2014-11-30-mediator_features/night-track.JPG
image2: /assets/article_images/2014-11-30-mediator_features/night-track-mobile.JPG
---
### **Reflections on Database Systems: A Journey Through Unit 1**

Before I started this module, my understanding of databases was limited. I considered databases to be simply collections of data in tables for the primary purpose of organizing data and retrieving information. But after the completion of Unit 1 in Database Systems Fundamentals, my perspective has changed significantly.

### **Learning the Purpose of Database Systems**
Initially, I believed that a database was just an electronic version of an Excel sheet. But now I understand that databases are far more advanced and powerful. A database system is not just storing data; it is designed to manage large volumes of data in an efficient way, maintain consistency, and offer data security. The structured nature of databases allows numerous users and applications to read data simultaneously without compromising integrity.

![](/dbms.jpg)

### **Why Database Systems are Important ?**
Through various examples, I realized the significance of database systems in businesses. In banks, social networking websites, sales, and even government services, databases are of utmost importance in order to function effectively. Traditional file-processing systems have their own drawbacks like redundancy, inconsistency, and insecurity. Database management systems (DBMS) save the day by providing data consistency, preventing redundancy, and improving security.

### **Evolution of Database Systems**
I was particularly fascinated by the historical evolution of database systems. Database systems earlier in history were closely tied to physical storage. The introduction of relational databases, pioneered by Edgar F. Codd, ushered in a disciplined approach that completely revolutionized data management. Today, modern database systems support many models such as relational, NoSQL, and object-based databases, addressing a broad spectrum of applications.

### **Key Takeaways from Unit 1**
- **Database vs. File-Based Systems**: Traditional file systems are prone to redundancy and inconsistency, whereas databases ensure efficiency, scalability, and better data management.
- **Advantages of DBMS**: Improved security, data integrity, and concurrent access make DBMS a preferred choice over simple data storage solutions.
- **Real-World Applications**: Almost every industry, from banking to healthcare, relies on robust database systems for decision-making and operations.


## **Views of Data in a DBMS**

![](/view_level.png)

A general-purpose DBMS supports multiple functionalities, such as data creation, querying, updating, and administration, based on a **data model**. These views help different users interact with data at different levels:

1. **Physical Level** – Describes how data is stored.
2. **Logical Level** – Describes what data is stored and their relationships.
3. **View Level** – Presents only a part of the database to specific users.

---
## **Types of Data Models**

A **data model** is a conceptual framework for describing data and its relationships. There are several types:

1. **Entity-Relationship (ER) Model** – Represents data in terms of entities, attributes, and relationships.
2. **Semi-Structured Data Model** – Used for data that doesn’t fit into traditional tables, such as JSON or XML.
3. **Object-Based Data Model** – Integrates object-oriented principles into databases.
4. **Relational Model** – Represents data in tables (relations) with rows and columns.

The **Relational Model** is the most commonly used data model in modern database systems.

![](/relational.png)

### **SQL and the Relational Model**
Structured Query Language (SQL) is the standard language for interacting with relational databases. It supports:
- **Data Definition Language (DDL)** – Used for defining database schema.
- **Data Manipulation Language (DML)** – Used for querying and modifying data.

Example of a **DDL command**:
```sql
CREATE TABLE department (
    dept_name CHAR(20) NOT NULL,
    building CHAR(15),
    budget NUMERIC(12,2)
);
```
Example of a **DML command**:
```sql
SELECT * FROM department WHERE budget > 50000;
```

---


## **Database System Architecture**
![](/architecture.png)
A **DBMS architecture** consists of several components that work together:

1. **Storage Manager** – Handles data storage and retrieval.
2. **Query Processor** – Interprets and executes SQL queries.
3. **Transaction Manager** – Ensures data consistency and handles concurrency.

Most modern applications interact with databases through an **Application Programming Interface (API)**, such as Open Database Connectivity (ODBC).

---

### **Homeworks**
1. Difference between `Database` and `Database Management System`.

![](/homework1.jpg)

2. Draw an `Entity Relational Diagram` for the student registration system at CST

![](/hw2.jpg)

---
### **Conclusion**
I appreciate the intricacies of data management and importance of structured, secure, and scalable database solutions. In further units in this module DBS101, I look forward to studying advanced topics like database design, relational models, and query languages to enhance my knowledge and practical skills.

