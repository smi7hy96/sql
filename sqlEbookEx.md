# SQL EBOOK EXERCISE

## CREATE TABLES

``` SQL
use ryan_db

-- USER --> ID (PK), Email, phone no., name
-- EBOOKS --> ID(PK), title, location, release date, user(FK)
-- BOOKING --> ID(PK), book(FK), user(FK), date, price

CREATE TABLE Users
(
users_ID INT NOT NULL IDENTITY(1,1) PRIMARY KEY,
first_name VARCHAR(20),
last_name VARCHAR(20),
email VARCHAR(100),
phone_No VARCHAR(15)
);

CREATE TABLE EBooks
(
ebook_ID INT NOT NULL IDENTITY(1,1) PRIMARY KEY,
title VARCHAR(40),
location VARCHAR(40),
release_date DATE,
users_ID int,
CONSTRAINT fk_users_ID FOREIGN KEY (users_ID) REFERENCES Users(users_ID)
);

CREATE TABLE Booking(
booking_ID INT NOT NULL IDENTITY(1,1) PRIMARY KEY,
ebook_ID int,
users_ID int,
booking_date date,
booking_price int,
CONSTRAINT fk_users_ID_bk FOREIGN KEY (users_ID) REFERENCES Users(users_ID),
CONSTRAINT fk_ebook_ID FOREIGN KEY (ebook_ID) REFERENCES Ebooks(ebook_ID)
);

```
