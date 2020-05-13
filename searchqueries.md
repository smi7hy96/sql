## SQL Search Query Examples
``` SQL
USE Northwind

--SELECT ALL
SELECT * FROM Employees

--COUNT NO. OF EMPLOYEES THAT MATCH SEARCH PARAM
SELECT COUNT (EmployeeID) AS 'Employee Count'
FROM Employees
WHERE City = 'London'

--SELECT CERTAIN COLUMNS
SELECT FirstName, LastName FROM Employees
WHERE TitleOfCourtesy = 'Dr.'

--COUNT EXAMPLE AGAIN
SELECT COUNT (ProductID) AS 'No. of Discontinued Products'
FROM Products
WHERE Discontinued = 1

--SELECT COLUMNS AGAIN
SELECT CompanyName, City, Country, Region
FROM Customers
WHERE Region = 'BC'

--WILDCARD CHARACTER TO USE '' IN OPERATION
SELECT * FROM Suppliers
WHERE CompanyName Like '%''%'

--SELECT COLUMNS AGAIN
SELECT CustomerID, City
FROM Customers
WHERE Country = 'France'

--SELECT TOP 100 WITH ORDER BY COLUMN
SELECT TOP 100 CompanyName, City
FROM Customers
WHERE Country = 'FRANCE'
ORDER BY City ASC

--DOUBLE WHERE CONDITION
SELECT ProductName, UnitPrice
FROM Products
WHERE CategoryID = 1 AND Discontinued = 0

--COMPARATORS (GREATER THAN)
SELECT ProductName, UnitPrice
FROM Products
WHERE UnitsInStock > 0 OR  UnitPrice > 29.99

--SELECT DISTINCT - only return unique results
SELECT DISTINCT Country
FROM Customers
WHERE ContactTitle = 'Owner'

--WILDCARD USES
SELECT DISTINCT Country
FROM Customers
WHERE ContactTitle = 'Owner' AND Country LIKE '_E%'
-- RULES
-- underscore = 1 character, % = any no. of characters,
-- [xyz]% = containing x, y, or z as the letter,
-- %[^zyx] = not ending in z, y or x

SELECT ProductName
FROM Products
WHERE ProductName LIKE 'Ch%'

SELECT *
FROM Customers WHERE Region LIKE '_A'

-- Checking for multiple values from the same column
SELECT *
FROM Customers WHERE Region IN ('WA', 'SP') --

-- SEARCH BETWEEN TWO VALUES
SELECT *
FROM EmployeeTerritories
WHERE TerritoryID BETWEEN 06800 AND 09999

-- COMPARATOR AGAIN
SELECT ProductName, ProductID
FROM Products
WHERE UnitPrice < 5.00

--WILDCARD USES - CHECKING FOR MULTIPLE CHARACTERS
SELECT CategoryName
FROM Categories
WHERE CategoryName LIKE '[bs]%'

--HAVING INSTEAD OF WHERE
SELECT EmployeeID, COUNT (*) AS "Number of Orders"
FROM Orders
GROUP BY EmployeeID
HAVING EmployeeID IN (5,7) --> used in place of WHERE when grouping results (GROUP BY)

--CONCATENATION
SELECT CompanyName AS 'Company Name', City + ',' + Country AS 'City' -- Concatenation of results together to produce location. AS renames the columnheading
FROM Customers

--MORE CONCATENATION
SELECT FirstName + ' ' + LastName AS "Employee Name"
FROM Employees

--IS NULL
SELECT Region, CompanyName AS 'Company Name', City + ',' + Country AS 'City'
FROM Customers
WHERE Region IS NULL

--IS NOT NULL
SELECT DISTINCT Country
FROM Customers
WHERE Region IS NOT NULL

```
### Joins
Joins are when you do a search query from multiple tables to get matching data from both.

![JOIN DIAGRAM](https://blog.codinghorror.com/content/images/uploads/2007/10/6a0120a85dcdae970b012877702708970c-pi.png)

    - (INNER) JOIN: Returns records that have matching values in both tables
    - LEFT (OUTER) JOIN: Returns all records from the left table, and the matched records from the right table
    - RIGHT (OUTER) JOIN: Returns all records from the right table, and the matched records from the left table
    - FULL (OUTER) JOIN: Returns all records when there is a match in either left or right table
