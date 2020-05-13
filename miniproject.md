# MINI PROJECT

## EXCERCISE ONE

``` SQL
-- 1.1 LIST ALL CUSTOMERS IN PARIS OR LONDON
SELECT c.CustomerID, c.CompanyName, c.Address + ', ' + c.City + ', ' + c.PostalCode AS "Address"
FROM Customers c
WHERE c.City IN ('Paris','London')

-- 1.2 LIST ALL PRDOUCTS STORED IN BOTTLES
SELECT *
FROM Products p
WHERE p.QuantityPerUnit LIKE '%bottles%'

-- 1.3 SEE 1.2 INCLUDING SUPPLIER NAME & COUNTRY
SELECT p.ProductID, p.ProductName, p.QuantityPerUnit, p.SupplierID, s.CompanyName, s.Country
FROM Products p
INNER JOIN Suppliers s ON p.SupplierID = s.SupplierID
WHERE p.QuantityPerUnit LIKE '%bottles%'

-- 1.4 HOW MANY PRODUCTS IN EACH CATEGORY - INCLUDE CAT. NAME - LIST HIGHEST FIRST

SELECT c.CategoryID, c.CategoryName, COUNT(p.ProductID) AS "Number of Products"
FROM Products p
INNER JOIN Categories c ON p.CategoryID = c.CategoryID
GROUP BY c.CategoryID, c.CategoryName
ORDER BY [Number of Products] DESC

-- 1.5 ALL UK EMPLOYEES - CONCAT TITLE, F&L NAME, INCLUDE CITY

SELECT e.TitleOfCourtesy + ' ' + e.FirstName + ' ' + e.LastName AS "Employee Name", e.City
FROM Employees e
WHERE e.Country = 'UK'

--1.6 SALES TOTALS FOR ALL REGIONS (VIA TERRITORIES - 4 JOINS) WITH TOTAL SALE > 1M. USE rounding or FORMAT to present numbers

SELECT c.Region, FORMAT((SUM(od.Quantity * od.UnitPrice * (1-od.Discount))), '##,##0') AS "Total Sales"
FROM Territories t
INNER JOIN EmployeeTerritories et ON t.TerritoryID = et.TerritoryID
INNER JOIN Employees e ON et.EmployeeID = e.EmployeeID
INNER JOIN Orders o ON e.EmployeeID = o.EmployeeID
INNER JOIN Customers c ON o.CustomerID = c.CustomerID
INNER JOIN [Order Details] od ON o.OrderID = od.OrderID
GROUP BY c.Region
--HAVING SUM(od.Quantity * od.UnitPrice * (1-od.Discount)) > 1000000
ORDER BY (SUM(od.Quantity * od.UnitPrice * (1-od.Discount))) DESC
-- territories -->  EmployeeTerritories (terriryID)      -->    Employees (empNo)       -->    order  (empNo)    --> order details (orderID)

-- 1.7 COUNT ORDERS THAT HAVE FREIGHT AMOUNT GREATER THAN 100.00 abd UK OR USA AS SHIP COUNTRY

SELECT COUNT(o.OrderID) AS "Freight Amount Count"
FROM Orders o
WHERE o.Freight > 100 AND o.ShipCountry IN ('UK', 'USA')

-- 1.8 IDENTIFY ORDER NUMBER OF THE ORDER WITH HIGHEST AMOUNT OF DISCOUNT APPLIED TO ORDER

SELECT TOP 1 od.OrderID, (od.Quantity * od.UnitPrice * od.Discount) AS "Amount Discounted"
FROM [Order Details] od
ORDER BY "Amount Discounted" DESC

```
## EXCERCISE TWO
``` SQL
USE ryan_db

CREATE TABLE Spartans
(
    Spartan_ID int NOT NULL IDENTITY(1,1) PRIMARY KEY,
    Title VarChar(30),
    First_Name VARCHAR(20),
    Last_Name VARCHAR(20),
    University VARCHAR(40),
    Course VARCHAR(30),
    Grade VARCHAR (10),
    Grad_Year INT
)

INSERT INTO Spartans
VALUES(
    'Mr', 'Ryan', 'Smith', 'Kingston University', 'Computer Science', 'First', 2019
)


INSERT INTO Spartans(
    Title, First_Name, Last_Name
) VALUES(
    'Mr', 'Fahad', 'Khisaf'
),
(
    'Mr', 'Marcus', 'Westhuizen'
),
(
    'Mr', 'Patrick', 'Clancy'
),
(
    'Mr', 'Stefan', 'Okolo'
),
(
    'Mr', 'Jonathan', 'Holder'
),
(
    'Mr', 'Nathan', 'Forester'
),
(
    'Mr', 'Avraj', 'Singh'
),
(
    'Mr', 'Ashraf', 'Mohamud'
),
(
    'Mr', 'Hussain', 'Ali Khan'
),
(
    'Miss', 'Saskia', 'Van Barthold'
),
(
    'Mr', 'Mergim', 'Berisha'
),
(
    'Mr', 'Delvin', 'Roy'
),
(
    'Mr', 'Samir', 'Djaafer'
)

SELECT * FROM Spartans
```
