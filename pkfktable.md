## Database and Table set up

### Day Two - Customer & Order Table

Looking at Primary & Foreign Key in tables with basic search params.
``` SQL
CREATE TABLE Customer
(
    customer_ID int NOT NULL IDENTITY(1,1) PRIMARY KEY,
    first_name VARCHAR(20),
    last_name VARCHAR(20),
    phone_No VARCHAR(15)
    );

CREATE TABLE Orders
(
    order_ID int NOT NULL IDENTITY(1,1) PRIMARY KEY,
    order_No INT NOT NULL,
    customer_ID int,
    CONSTRAINT fk_customer_ID FOREIGN KEY (customer_ID)
    REFERENCES Customer(customer_ID)
    );

ALTER TABLE Orders
    DROP CONSTRAINT fk_customer_ID;

ALTER TABLE Orders
    ADD CONSTRAINT fk_cust_ID
    FOREIGN KEY (customer_ID)
    REFERENCES Customer(customer_ID)
    ON DELETE CASCADE;


SP_HELP Customer
SP_HELP Orders

INSERT INTO Customer(
    first_name, last_name
)
VALUES
/*(
    'Ryan', 'Smith'
), */
(
    'Jason', 'Statham'
);

INSERT INTO Orders(
    order_No, customer_ID
)
VALUES
/*(
    '2563', '1'
),*/
(
    '1586', '3'
);

SELECT * FROM Customer;

SELECT * FROM Orders;


SELECT first_name
FROM Orders
INNER JOIN Customer ON Orders.customer_ID = Customer.customer_ID;


DELETE FROM Customer WHERE customer_ID = 2;
```
