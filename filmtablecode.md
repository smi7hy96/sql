## Database and Table set up

### Day One - film table
``` sql
USE Northwind

CREATE DATABASE ryan_db;

USE ryan_db

CREATE TABLE film_table
(
    film_id int IDENTITY(1,1) PRIMARY KEY,
    film_name VARCHAR(20),
    film_type VARCHAR(10),
    date_of_release date,
    director VARCHAR(20),
    writer VARCHAR(20),
    rating DECIMAL(2,1),
    film_language VARCHAR(15),
    website VARCHAR(255),
    plot_Summ VARCHAR(max),
    )

SP_HELP film_table

DROP TABLE film_table

ALTER TABLE film_table
    ADD star int;

ALTER TABLE film_table
    ALTER COLUMN film_name VARCHAR(45) NOT NULL;

ALTER TABLE film_table
    DROP COLUMN star;

INSERT INTO film_table(
    film_name, film_type
)
VALUES
(
    'Blue Streak', 'Action'
),
(
    'Long Shot', 'Comedy'
);

SELECT * FROM film_table;

UPDATE film_table
SET    director = 'Peter Jackson', rating = 5
WHERE film_id = 1;

```
