# SQL

Structured Query Language is the standard language for databases and allows access to modify/ view tables and values in databses using queries.  It can be used in tandem with other languages such as PHP in websites.

## Basic SQL Commands

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
