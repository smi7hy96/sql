# SQL

Structured Query Language is the standard language for databases and allows access to modify/ view tables and values in databses using queries.  It can be used in tandem with other languages such as PHP in websites.

## Basic SQL Commands

![JOIN DIAGRAM](https://i.stack.imgur.com/7uUaJ.png)

### DML - Record Manipulation
- INSERT - Add a new record into a table
  - INSERT INTO *table_name* (*column1*, *column2*)
    VALUES ('*value1*', '*value2*')

- DELETE - Delete existing records from a table
  - DELETE FROM *table_name* WHERE *condition*  (Delete certain records)
  - DELETE FROM *table_name* (Delete all records)

- UPDATE - Modify existing records in a table
  - UPDATE *table_name*
    SET *column1* = '*value1*', *column2* = *value2'*
    WHERE *condition*
- SELECT - Search and retrieve data from a database/ table
  - SELECT * FROM *table_name*;
  - SELECT *column1*, *column2*
    FROM *table_name*;

### DDL - Structure Manipulation
- CREATE TABLE *table_name* () - create table
  - *column_name* DATATYPE
    - int IDENTITY(1,1) PRIMARY KEY -> auto-increment integer and use as Primary Key
    - int(*x*) --> normal integer
    - CHAR(*x*) --> Characters of fixed length *x*. Will use fixed memory regardless of input length
    - VARCHAR(*x*) --> Upper range of Character length set (*x*). Will use input length of memory
    - date --> date format value
    - DECIMAL(*x*, *y*) --> Decimal number where total no. of digits = *x* and decimal place amount = *y*

- ALTER TABLE *table_name* - make change to strucutre of table either adding/ removing column or changing colun syntax

- DROP TABLE - delete existing table
    - DROP COLUMN can also be used (within ALTER TABLE) to remove column instead
