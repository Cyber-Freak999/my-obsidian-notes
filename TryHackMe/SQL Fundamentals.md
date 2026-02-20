---
tags:
  - concept
link: https://tryhackme.com/room/sqlfundamentals
---
# Database
Databases are an organised collection of structured information or data that is easily accessible and can be manipulated or analysed.
## Common Types of Database
**Relational databases:** Store structured data, meaning the data inserted into this database follows a structure. For example, the data collected on a user consists of first_name, last_name, email_address, username and password. When a new user joins, an entry is made in the database following this structure. This structured data is stored in rows and columns in a table (all of which will be covered shortly); relationships can then be made between two or more tables (for example, user and order_history), hence the term relational databases.

**Non-relational databases:** Instead of storing data the above way, store data in a non-tabular format. For example, if documents are being scanned, which can contain varying types and quantities of data, and are stored in a database that calls for a non-tabular format.
```bash
 {
    _id: ObjectId("4556712cd2b2397ce1b47661"),
    name: { first: "Thomas", last: "Anderson" },
    date_of_birth: new Date('Sep 2, 1964'),
    occupation: [ "The One"],
    steps_taken : NumberLong(4738947387743977493)
}
```

## Tables, Columns and Rows
All data stored in a relational database will be stored in a **table**. When creating this table, you would need to define what pieces of information are needed to define a book record, for example, “id”, “Name”, and “Published_date”. These would then be your **columns**; when these columns are being defined, you would also define what data type this column should contain; if an attempt is made to insert a record into a database where the data type does not match, it is rejected.
Once a table has been created with the columns defined, the first record would be inserted into the database, for example, a book named “Android Security Internals” with an id of “1” and a publication date of “2014-10-14”. Once inserted, this record would be represented as a **row**.
## Primary and Foreign Keys
**Primary Keys**: A primary key is used to ensure that the data collected in a certain column is unique. That is, there needs to be a way to identify each record stored in a table, a value unique to that record and is not repeated by any other record in that table. Think about matriculation numbers in a university; these are numbers assigned to a student so they can be uniquely identified in records (as sometimes students can have the same name). A column has to be chosen in each table as a primary key; in our example, “id” would make the most sense as an id has been uniquely created for each book where, as books can have the same publication date or (in rarer cases) book title. Note that there can only be one primary key column in a table.

**Foreign Keys**: A foreign key is a column (or columns) in a table that also exists in another table within the database, and therefore provides a link between the two tables. In our example, think about adding an “author_id” field to our “Books” table; this would then act as a foreign key because the author_id in our Books table corresponds to the “id” column in the author table. Foreign keys are what allow the relationships between different tables in relational databases. Note that there can be more than one foreign key column in a table.
# SQL
Databases are usually controlled using a Database Management System (DBMS). Serving as an interface between the end user and the database, a DBMS is a software program that allows users to retrieve, update and manage the data being stored. Some examples of DBMSs include MySQL, MongoDB, Oracle Database and Maria DB. 
The interaction between the end user and the database can be done using SQL (Structured Query Language). SQL is a programming language that can be used to query, define and manipulate the data stored in a relational database. 
SQL is almost as ubiquitous as databases themselves, and for good reason. Here are some of the benefits that come with learning and using to use SQL:  
- **It's _fast_** 
- **Easy to Learn**
- **Reliable** 
- **Flexible**

# Database Statements
## CREATE DATABASE
If a new database is needed, the first step you would take is to create it. This can be done in SQL using the `CREATE DATABASE` statement. This would be done using the following syntax: `CREATE DATABASE database_name;`
### **SHOW DATABASES**
Now that we have created a database, we can view it using the `SHOW DATABASES` statement. The `SHOW DATABASES` statement will return a list of present databases. Run the statement as follows: `mysql> SHOW DATABASES;`
## USE DATABASE
Once a database is created, you may want to interact with it. Before we can interact with it, we need to tell mysql which database we would like to interact with (so it knows which database to run subsequent queries against). To set the database we have just created as the active database, we would run the `USE` statement as follows (make sure to run this on your machine): `USE databse_name;`
## DROP DATABASE
Once a database is no longer needed (maybe it was created for test purposes, or is no longer required), it can be removed using the `DROP` statement. To remove a database, we would use the following statement syntax (although, in our case, we want to keep our database, so no need to run this one yourself!): `mysql> DROP database database_name;`
# Table Statements
## CREATE TABLE
Following the logic of the database statements, creating tables also uses a `CREATE` statement. Once a database is active (you have run the `USE` statement on it), a table can be created within it using the following statement syntax: 
```sql
CREATE TABLE example_table_name (
     example_column1 data_type,
     example_column2 data_type,
     example_column3 data_type
);
```

Example:
```sql
 CREATE TABLE book_inventory (
    book_id INT AUTO_INCREMENT PRIMARY KEY,
    book_name VARCHAR(255) NOT NULL,
    publication_date DATE
);
```
## **SHOW TABLES** 
Just as we can list databases using a SHOW statement, we can also list the tables in our currently active database (the database on which we last used the USE statement). Run the following command, and you should see the table you have just created: `SHOW TABLES;`
## **DESCRIBE** 
If we want to know what columns are contained within a table (and their data type), we can describe them using the `DESCRIBE` command (which can also be abbreviated to `DESC`). Describe the table you have just created using the following command:`DESCRIBE table_name;`
## **ALTER** 
Once you have created a table, there may come a time when your need for the dataset changes, and you need to alter the table. This can be done using the `ALTER` statement. Let’s now imagine that we have decided that we actually want to have a column in our book inventory that has the page count for each book. Add this to our table using the following statement: 
```sql
ALTER TABLE book_inventory 
ADD page_count INT;
```
## DROP 
Similar to removing a database, you can also remove tables using the `DROP` statement. We don’t need to do this, but the syntax you would use for this is: `DROP TABLE table_name;`
# CRUD Operations
## Create Operation (INSERT)
The **Create** operation will create new records in a table. In MySQL, this can be achieved by using the statement `INSERT INTO`, as shown below.  
```shell-session
mysql> INSERT INTO books (id, name, published_date, description)
    VALUES (1, "Android Security Internals", "2014-10-14", "An In-Depth Guide to Android's Security Architecture");

Query OK, 1 row affected (0.01 sec)
```

As we can observe, the `INSERT INTO` statement specifies a table, in this case, **books**, where you can add a new record; the columns **id**, **name**, **published_date**, and **description** are the records in the table. In this example, a new record with an **id** of  **1**, a **name** of **"Android Security Internals**", a **published_date** of "**2014-10-14**", and a **description** stating "**Android Security Internals provides a complete understanding of the security internals of Android devices**" was added.
## Read Operation (SELECT)
The **Read** operation, as the name suggests, is used to read or retrieve information from a table. We can fetch a column or all columns from a table with the `SELECT` statement, as shown in the next example.  
## Update Operation (UPDATE)
The **Update** operation modifies an existing record within a table, and the same statement, `UPDATE`, can be used for this.  
```shell-session
mysql> UPDATE books
    SET description = "An In-Depth Guide to Android's Security Architecture."
    WHERE id = 1;

Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0     
```
The `UPDATE` statement specifies the table, in this case, **books**, and then we can use `SET` followed by the column name we will update. The `WHERE` clause specifies which row to update when the clause is met, in this case, the one with **id 1**.
## Delete Operation (DELETE)
The **delete** operation removes records from a table. We can achieve this with the `DELETE` statement.
```shell-session
mysql> DELETE FROM books WHERE id = 1;

Query OK, 1 row affected (0.00 sec)    
```
Above, we can observe the `DELETE` statement followed by the `FROM` clause, which allows us to specify the table where the record will be removed, in this case, **books**, followed by the `WHERE` clause that indicates that it should be the one where the **id** is **1**.
# Clauses
A clause is a part of a statement that specifies the criteria of the data being manipulated, usually by an initial statement. Clauses can help us define the type of data and how it should be retrieved or sorted.
## DISTINCT Clause
The `DISTINCT` clause is used to avoid duplicate records when doing a query, returning only unique values.
```shell-session
mysql> SELECT * FROM books;
+----+----------------------------+----------------+--------------------------------------------------------+
| id | name                       | published_date | description                                            |
+----+----------------------------+----------------+--------------------------------------------------------+
|  1 | Android Security Internals | 2014-10-14     | An In-Depth Guide to Android's Security Architecture   |
|  2 | Bug Bounty Bootcamp        | 2021-11-16     | The Guide to Finding and Reporting Web Vulnerabilities |
|  3 | Car Hacker's Handbook      | 2016-02-25     | A Guide for the Penetration Tester                     |
|  4 | Designing Secure Software  | 2021-12-21     | A Guide for Developers                                 |
|  5 | Ethical Hacking            | 2021-11-02     | A Hands-on Introduction to Breaking In                 |
|  6 | Ethical Hacking            | 2021-11-02     |                                                        |
+----+----------------------------+----------------+--------------------------------------------------------+

6 rows in set (0.00 sec)
```

```shell-session
mysql> SELECT DISTINCT name FROM books;
+----------------------------+
| name                       |
+----------------------------+
| Android Security Internals |
| Bug Bounty Bootcamp        |
| Car Hacker's Handbook      |
| Designing Secure Software  |
| Ethical Hacking            |
+----------------------------+

5 rows in set (0.00 sec)
```
## GROUP BY Clause
The `GROUP BY` clause aggregates data from multiple records and **groups** the query results in columns. This can be helpful for aggregating functions.  
```shell-session
mysql> SELECT name, COUNT(*)
    FROM books
    GROUP BY name;
+----------------------------+----------+
| name                       | COUNT(*) |
+----------------------------+----------+
| Android Security Internals |        1 |
| Bug Bounty Bootcamp        |        1 |
| Car Hacker's Handbook      |        1 |
| Designing Secure Software  |        1 |
| Ethical Hacking            |        2 |
+----------------------------+----------+

5 rows in set (0.00 sec)
```

In the example above, the records on the **book** table are regrouped by the result of the `COUNT` function. We already know that **Ethical hacking** is listed twice, so the total **count** is 2, placed at the end since it is **grouped** **by** count.
## ORDER BY Clause
The `ORDER BY` clause can be used to sort the records returned by a query in ascending or descending order. Using functions like `ASC` and `DESC` can help us to accomplish that, as shown below in the next two examples.
**ASCENDING ORDER**
```shell-session
mysql> SELECT *
    FROM books
    ORDER BY published_date ASC;
+----+----------------------------+----------------+--------------------------------------------------------+
| id | name                       | published_date | description                                            |
+----+----------------------------+----------------+--------------------------------------------------------+
|  1 | Android Security Internals | 2014-10-14     | An In-Depth Guide to Android's Security Architecture   |
|  3 | Car Hacker's Handbook      | 2016-02-25     | A Guide for the Penetration Tester                     |
|  5 | Ethical Hacking            | 2021-11-02     | A Hands-on Introduction to Breaking In                 |
|  6 | Ethical Hacking            | 2021-11-02     |                                                        |
|  2 | Bug Bounty Bootcamp        | 2021-11-16     | The Guide to Finding and Reporting Web Vulnerabilities |
|  4 | Designing Secure Software  | 2021-12-21     | A Guide for Developers                                 |
+----+----------------------------+----------------+--------------------------------------------------------+

6 rows in set (0.00 sec)
```

**DESCENDING ORDER**
```shell-session
mysql> SELECT *
    FROM books
    ORDER BY published_date DESC;
+----+----------------------------+----------------+--------------------------------------------------------+
| id | name                       | published_date | description                                            |
+----+----------------------------+----------------+--------------------------------------------------------+
|  4 | Designing Secure Software  | 2021-12-21     | A Guide for Developers                                 |
|  2 | Bug Bounty Bootcamp        | 2021-11-16     | The Guide to Finding and Reporting Web Vulnerabilities |
|  5 | Ethical Hacking            | 2021-11-02     | A Hands-on Introduction to Breaking In                 |
|  6 | Ethical Hacking            | 2021-11-02     |                                                        |
|  3 | Car Hacker's Handbook      | 2016-02-25     | A Guide for the Penetration Tester                     |
|  1 | Android Security Internals | 2014-10-14     | An In-Depth Guide to Android's Security Architecture   |
+----+----------------------------+----------------+--------------------------------------------------------+

6 rows in set (0.00 sec)
```

## HAVING Clause
The `HAVING` clause is used with other clauses to filter groups or results of records based on a condition. In the case of `GROUP BY`, it evaluates the condition to `TRUE` or `FALSE`, unlike the `WHERE` clause `HAVING` filters the results after the aggregation is performed.  
```shell-session
mysql> SELECT name, COUNT(*)
    FROM books
    GROUP BY name
    HAVING name LIKE '%Hack%';
+-----------------------+----------+
| name                  | COUNT(*) |
+-----------------------+----------+
| Car Hacker's Handbook |        1 |
| Ethical Hacking       |        2 |
+-----------------------+----------+

2 rows in set (0.00 sec)
```
# Operators
## Logical Operators

These operators test the truth of a condition and return a boolean value of `TRUE` or `FALSE`. Let's explore some of these operators next.  

## LIKE Operator
The `LIKE` operator is commonly used in conjunction with clauses like `WHERE` in order to filter for specific patterns within a column. Let's continue using our DataBase to query an example of its usage.  
```shell-session
mysql> SELECT *
    FROM books
    WHERE description LIKE "%guide%";
```
The query above returns a list of records from the books filtered, but the ones using the `WHERE` clause that contains the word guide by using the `LIKE` operator.  
## AND Operator
The `AND` operator uses multiple conditions within a query and returns `TRUE` if all of them are true.  
```shell-session
mysql> SELECT *
    FROM books
    WHERE category = "Offensive Security" AND name = "Bug Bounty Bootcamp";   
```

The query above returns the book with the name **Bug Bounty Bootcamp**, which is under the category of **Offensive Security**.  
## OR Operator
The `OR` operator combines multiple conditions within queries and returns `TRUE` if at least one of these conditions is true.  
```shell-session
mysql> SELECT *
    FROM books
    WHERE name LIKE "%Android%" OR name LIKE "%iOS%"; 
```

The query above returns books whose **names** include either **Android** or **IOS**.  
## NOT Operator
The `NOT` operator reverses the value of a boolean operator, allowing us to exclude a specific condition.  
```shell-session
mysql> SELECT *
    FROM books
    WHERE NOT description LIKE "%guide%";
```
 
The query above returns results where the description does not contain the word **guide**.  
## BETWEEN Operator
The `BETWEEN` operator allows us to test if a value exists within a defined **range**.  
```shell-session
mysql> SELECT *
    FROM books
    WHERE id BETWEEN 2 AND 4;
```

The query above returns books whose **id** is **between 2** and **4**.
## Comparison Operators
The comparison operators are used to compare values and check if they meet specified criteria.  
### Equal To Operator
The `=` (Equal) operator compares two expressions and determines if they are equal, or it can check if a value matches another one in a specific column.  
```shell-session
mysql> SELECT *
    FROM books
    WHERE name = "Designing Secure Software";
```
 
The query above returns the book with the **exact name Designing Secure Software**.
### Not Equal To Operator
The `!=` (not equal) operator compares expressions and tests if they are not equal; it also checks if a value differs from the one within a column.  
```shell-session
mysql> SELECT *
    FROM books
    WHERE category != "Offensive Security";
```

The query above returns books **except** those whose **category** is **Offensive Security**.
### Less Than Operator
The `<` (less than) operator compares if the expression with a given value is lesser than the provided one.
```shell-session
mysql> SELECT *
    FROM books
    WHERE published_date < "2020-01-01";
```

The query above returns books that were published **before January 1, 2020**.
### Greater Than Operator
The `>` (greater than) operator compares if the expression with a given value is greater than the provided one.  
```shell-session
mysql> SELECT *
    FROM books
    WHERE published_date > "2020-01-01";
```

The query above returns books published **after** **January 1, 2020**.
### Less Than or Equal To and Greater  Than or Equal To Operators
The `<=` (Less than or equal) operator compares if the expression with a given value is less than or equal to the provided one. On the other hand, The `>=` (Greater than or Equal) operator compares if the expression with a given value is greater than or equal to the provided one. Let's observe some examples of both below.  
```shell-session
mysql> SELECT *
    FROM books
    WHERE published_date <= "2021-11-15";
```

The query above returns books **published on** **or before** **November 15, 2021**.

```shell-session
mysql> SELECT *
    FROM books
    WHERE published_date >= "2021-11-02";
```

The query above returns books that were **published on or after November 2, 2021**.
# Functions
## String Functions
Strings functions perform operations on a string, returning a value associated with it.
### CONCAT() Function
This function is used to add two or more strings together. It is useful to combine text from different columns.  
```shell-session
mysql> SELECT CONCAT(name, " is a type of ", category, " book.") AS book_info FROM books;
+------------------------------------------------------------------+
| book_info                                                         |
+------------------------------------------------------------------+
| Android Security Internals is a type of Defensive Security book. |
| Bug Bounty Bootcamp is a type of Offensive Security book.        |
| Car Hacker's Handbook is a type of Offensive Security book.      |
| Designing Secure Software is a type of Defensive Security book.  |
| Ethical Hacking is a type of Offensive Security book.            |
+------------------------------------------------------------------+

5 rows in set (0.00 sec)  
```

This query concatenates the **name** and **category** columns from the **books** table into a single one named **book_info**.

### GROUP_CONCAT() Function
This function can help us to concatenate data from multiple rows into one field. Let's explore an example of its usage.  
```shell-session
mysql> SELECT category, GROUP_CONCAT(name SEPARATOR ", ") AS books
    FROM books
    GROUP BY category;
```

The query above groups the **books** by **category** and concatenates the titles of books within each category into a **single string**.
### SUBSTRING() Function
This function will retrieve a substring from a string within a query, starting at a determined position. The length of this substring can also be specified.  
```shell-session
mysql> SELECT SUBSTRING(published_date, 1, 4) AS published_year FROM books;
+----------------+
| published_year |
+----------------+
| 2014           |
| 2021           |
| 2016           |
| 2021           |
| 2021           |
+----------------+

5 rows in set (0.00 sec)  
```

In the query above, we can observe how it extracts the first **four** characters from the **published_date** column and stores them in the **published_year** column.

### LENGTH() Function
This function returns the number of characters in a string. This includes spaces and punctuation. We can find an example below.  
```shell-session
mysql> SELECT LENGTH(name) AS name_length FROM books;
+-------------+
| name_length |
+-------------+
|          26 |
|          19 |
|          21 |
|          25 |
|          15 |
+-------------+

5 rows in set (0.00 sec)  
```

As we can observe above, the query calculates the length of the string within the **name** column and stores it in a column named **name_length**.
## Aggregate Functions
These functions aggregate the value of multiple rows within one specified criteria in the query; It can combine multiple values into one result.

### COUNT() Function
This function returns the number of records within an expression, as the example below shows.  
```shell-session
mysql> SELECT COUNT(*) AS total_books FROM books;
+-------------+
| total_books |
+-------------+
|           5 |
+-------------+

1 row in set (0.01 sec)
```

This query above counts the total number of rows in the **books** table. The result is **5**, as there are five books in the books table, and it's stored in the **total_books** column.
### SUM() Function
This function sums all values (not NULL) of a determined column.
```shell-session
mysql> SELECT SUM(price) AS total_price FROM books;
+-------------+
| total_price |
+-------------+
|      249.95 |
+-------------+

1 row in set (0.00 sec)
```

The query above calculates the total sum of the **price** column. The result provides the aggregate price of all books in the column **total_price**.

### MAX() Function
This function calculates the maximum value within a provided column in an expression.  
```shell-session
mysql> SELECT MAX(published_date) AS latest_book FROM books;
+-------------+
| latest_book |
+-------------+
| 2021-12-21  |
+-------------+

1 row in set (0.00 sec)
```

The query above retrieves the latest publication (maximum value) date from the **books** table. The result **2021-12-21** is stored in the column **latest_book**.

### MIN() Function
This function calculates the minimum value within a provided column in an expression.  
```shell-session
mysql> SELECT MIN(published_date) AS earliest_book FROM books;
+---------------+
| earliest_book |
+---------------+
| 2014-10-14    |
+---------------+

1 row in set (0.00 sec)
```

The query above retrieves the earliest publication (minimum value) date from the **books** table. The result **2014-10-14** is stored in the **earliest_book** column.