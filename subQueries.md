# SUB-QUERIES

## Use queries within queries to produce data from multiple tables

``` SQL
use Northwind

-- SUB QUERY EXAMPLE --> using nested queries, similar method to joins EXCEPT PK/FK relationship not needed
SELECT c.CompanyName AS "Customer"
FROM Customers c
WHERE CustomerID NOT IN
(SELECT CustomerID FROM Orders)

-- Another sub query example, using the query to do a separate calculation - essentially a self join
SELECT od.OrderID, od.ProductID, od.UnitPrice, od.Quantity, od.Discount, (SELECT MAX(UnitPrice)
FROM [Order Details] od1) AS "Max Price"
FROM [Order Details] od

-- ADVANCED QUERY - selecting certain columns from the sub query and using them as a separate entity, retrieving limited results from second table
SELECT od.ProductID, sq1.totalamt as "Total Sold for this Product", UnitPrice, (UnitPrice*Quantity/totalamt*100) AS "% Of Total"
FROM [Order Details] od
INNER JOIN
(SELECT ProductID, SUM(UnitPrice * Quantity) AS totalamt
FROM [Order Details]
GROUP BY ProductID) sq1 ON sq1.ProductID = od.ProductID

-- Get Order details of products that are not discontiunued using sub query
SELECT od.OrderID, od.ProductID, od.UnitPrice, od.Quantity, od.Discount
FROM [Order Details] od
WHERE od.ProductID IN
(SELECT p.ProductID FROM Products p
WHERE p.Discontinued = 1)

-- Same as previous but instead using a join using the FK/PK relationship between the tables
SELECT od.OrderID, od.ProductID, od.UnitPrice, od.Quantity, od.Discount
FROM [Order Details] od
INNER JOIN Products p ON od.ProductID = p.ProductID
WHERE p.Discontinued = 1

-- UNION ALL - Combines result set from two SELECT STATEMENTS into ONE COLUMN.
-- Select columns must be of the same data type and there must be the same number of columns (in same order)
-- Custom Column Name will be from the original SELECT (ie. AS emp/supp ln. 38)
SELECT e.EmployeeID AS "Employee/Supplier"
FROM Employees e
UNION ALL -- Just UNION will remove duplicates and only give DISTINCT
SELECT s.SupplierID
FROM Suppliers s
```
