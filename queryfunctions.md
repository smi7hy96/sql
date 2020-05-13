## More Advance SELECT Query Functions
``` SQL
USE Northwind

-- Basic Arithmetic
SELECT UnitPrice, Quantity, Discount, UnitPrice * Quantity AS "Gross Total", UnitPrice * Quantity * (1-Discount) AS "NET TOTAL"
FROM [Order Details]

-- SORTING ORDER BY
SELECT UnitPrice, Quantity, Discount, UnitPrice * Quantity AS "Gross Total", UnitPrice * Quantity * (1-Discount) AS "NET TOTAL"
FROM [Order Details]
ORDER BY "NET TOTAL" DESC

-- Top 2 when ordered
SELECT TOP 2 OrderID,
UnitPrice * Quantity * (1 - Discount) AS "NET TOTAL"
FROM [Order Details]
ORDER BY "NET TOTAL" DESC

-- SUBSTRING - certain string of letters between parameters
SELECT SUBSTRING('SQL Tutorial', 1, 3) AS ExtractString;

-- CHARINDEX - certain character's position
SELECT CHARINDEX('m', 'Customer') AS MatchPosition;

-- LTRIM - Remove empty space left of string
SELECT LTRIM('     SQL Tutorial') AS LeftTrimmedString;

-- RTRIM - Remove space right of string
SELECT RTRIM('SQL Tutorial    ') AS RightTrimmedString;

-- REPLACE - replace certain character with another
SELECT REPLACE('SQL Tutorial', 'T', 'M');

--CHARINDEX EXAMPLE
SELECT PostalCode AS "Post Code",
LEFT(PostalCode, CHARINDEX(' ', PostalCode) - 1) AS "Post Code Region",
CHARINDEX(' ',PostalCode) AS "Space Found", Country
FROM Customers
WHERE Country = 'UK'

-- SELECT WHEN CONTAINING APOSTOPHE USING CHARINDEX
SELECT ProductName
FROM Products
WHERE CHARINDEX('''', ProductName) > 0

/*
GETDATE() --> return date and time
SYSDATETIME() --> return comp date and time
DATEADD(d,5,OrderDate) AS "Due Date" --> add duration to a date
DATEDIFFF(d, OrderDate, ShippedDate) AS "Ship Time" --> difference between dates
SELECT YEAR(OrderDate) AS "Order Year" --> extract year
SELECT MONTH(OrderDate) AS "Order Month" --> extract month
SELECT DAY(OrderDate) AS "Order Day" --> extract day
*/

-- Adding days to date and difference between
SELECT DATEADD(d,5, OrderDate) AS "Due Date",
DATEDIFF(d, OrderDate, ShippedDate) AS "Ship Days"
FROM Orders

-- getting age from DoB - Not completely accurate
SELECT FirstName + ' ' + LastName AS "Name",
DATEDIFF(yyyy, BirthDate, GETDATE()) AS "Age"
FROM Employees

-- getting age from DoB - Not completely accurate
SELECT FirstName + ' ' + LastName AS "Name",
DATEDIFF(yyyy, BirthDate, GETDATE()) AS "Age"
FROM Employees

-- FLOOR Rounds to nearest INT, more accurate (also switch yyyy to dd and divide by no. of days in year - leap year add .25)
SELECT FirstName + ' ' + LastName AS "Name",
FLOOR(DATEDIFF(dd, BirthDate, GETDATE())/365.25) AS "Age"
FROM Employees

-- USE CASE - basically if else statements checking whether delivery is delayed or not
SELECT DATEDIFF(d, OrderDate, ShippedDate) AS "Days for Delivery",
CASE
WHEN DATEDIFF(d, OrderDate, ShippedDate) <10
THEN 'On Time'
ELSE 'Overdue'
END AS "Status"
FROM Orders

-- ANOTHER USE CASE EXAMPLE
SELECT
CASE
WHEN FLOOR(DATEDIFF(dd, BirthDate, GETDATE())/365.25) > 65
THEN 'Retired'
WHEN FLOOR(DATEDIFF(dd, BirthDate, GETDATE())/365.25) = 60
THEN 'Retirement Due'
ELSE 'More than 5 years to go'
END AS 'Retirement Status'
FROM Employees

-- FILTERING FOR SUM, AVG, MIN and MAX of all Orders
SELECT SUM(UnitsOnOrder) AS "Total Order",
AVG(UnitsOnOrder) AS "Average Order",
MIN(UnitsOnOrder) AS "Min Order",
MAX(UnitsOnOrder) AS "Max Order"
FROM Products

-- FILTERING FOR SUM, AVG, MIN and MAX of all Orders INCLUDING GROUP BY TO GET INDIVIDUAL SUPPLIER ORDER FILTERS
SELECT SupplierID,
SUM(UnitsOnOrder) AS "Total Order",
AVG(UnitsOnOrder) AS "Average Order",
MAX(UnitsOnOrder) AS "Max Order"
FROM Products
GROUP BY SupplierID
ORDER BY "Average Order" DESC

-- ANOTHER GROUP BY EXAMPLE - TOP 1
SELECT TOP 1 CategoryID,
AVG(ReorderLevel) AS "Average Reorder"
FROM Products
GROUP BY CategoryID
ORDER BY "Average Reorder" DESC

-- USING GROUP BY CONDITIONS REQUIRES HAVING INSTEAD OF WHERE
SELECT SupplierID,
SUM(UnitsOnOrder) AS "Total on Order",
AVG(UnitsOnOrder) AS "Avg on Order"
FROM Products
GROUP BY SupplierID
HAVING AVG(UnitsOnOrder) > 5
ORDER BY "Total on Order" DESC

/*
    LOGICAL SYNTAX SEQUENCE
    SELECT
    DISTINCT
    FROM
    WHERE
    GROUP BY
    HAVING
    ORDER BY
    */
```
