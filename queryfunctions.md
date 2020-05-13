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
```
