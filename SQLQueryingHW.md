# QUERYING HOMEWORK

``` SQL
use Northwind

-- Q1 - How many orders in NWDB
SELECT COUNT(o.OrderID)
FROM Orders o

-- Q2 - How many ship from Rio De Janeiro
SELECT COUNT(o.OrderID)
FROM Orders o
WHERE o.ShipCity = 'Rio De Janeiro'

-- Q3 - Select all orders from Rio or Reims
SELECT *
FROM Orders o
WHERE o.ShipCity IN ('Rio De Janeiro', 'Reims')

-- Q4 - Select all entries where company name has a z or a Z in table of Customers
SELECT *
FROM Customers c
WHERE c.CompanyName LIKE ('%Z%')

-- Q5 All companies without fax info - display contact name, contact number and city
SELECT c.CustomerID, c.CompanyName, c.ContactName, c.Phone, c.Fax
FROM Customers c
WHERE c.Fax IS NULL

-- Q6 - Find Customer info for customers in paris
SELECT *
FROM Customers c
WHERE c.City = 'Paris'

-- Q7 - Find out who orders the most by quantity - top 5?? NOTE: There is only 2 custoemrs in paris and only one has an order history
SELECT TOP 5 c.CustomerID, c.ContactName, SUM(od.Quantity) AS "TOTAL Quantities Ordered"
FROM Customers c
INNER JOIN Orders o ON c.CustomerID = o.CustomerID
INNER JOIN [Order Details] od ON o.OrderID = od.OrderID
WHERE c.City = 'Paris'
GROUP BY c.CustomerID, c.ContactName
ORDER BY SUM(od.Quantity)

-- Q8 - Find out (from the previous list) number of orders that were over 10 days to ship. NOTE: no order took over 10 days to ship. SEE SECOND QUERY
SELECT TOP 5 c.CustomerID, c.ContactName, c.CompanyName, c.Phone, c.Address, SUM(od.TQuan) AS "TOTAL Quantities Ordered", COUNT(od.OrderID) AS "Orders Overdue"
FROM Customers c
INNER JOIN Orders o ON c.CustomerID = o.CustomerID
INNER JOIN (SELECT DISTINCT OrderID, SUM(Quantity) AS TQuan FROM [Order Details] GROUP BY OrderID) od ON od.OrderID = o.OrderID
WHERE c.City = 'Paris' AND DATEDIFF(dd, o.OrderDate, o.ShippedDate) > 0
GROUP BY c.CustomerID, c.ContactName, c.CompanyName, c.Phone, c.Address
ORDER BY SUM(od.TQuan)

--Proof no order takes over 10 days
SELECT o.OrderID, DATEDIFF(dd, o.OrderDate, o.ShippedDate) AS "Days Overdue"
FROM Orders o
WHERE o.CustomerID = 'SPECD' AND DATEDIFF(dd, o.OrderDate, o.ShippedDate) > 0

```
