# Joins
Joins are when you do a search query from multiple tables to get matching data from both.

![JOIN DIAGRAM](https://blog.codinghorror.com/content/images/uploads/2007/10/6a0120a85dcdae970b012877702708970c-pi.png)

    - (INNER) JOIN: Returns records that have matching values in both tables
    - LEFT (OUTER) JOIN: Returns all records from the left table, and the matched records from the right table
    - RIGHT (OUTER) JOIN: Returns all records from the right table, and the matched records from the left table
    - FULL (OUTER) JOIN: Returns all records when there is a match in either left or right table

``` SQL
-- INNER JOIN USING FOREIGN KEY (supplierID) to display both AVERAGE and Company Name in one table
SELECT p.SupplierID, s.CompanyName, AVG(p.UnitsOnOrder) AS "Average"
FROM Products p
INNER JOIN Suppliers s
ON p.SupplierID = s.SupplierID
GROUP BY p.SupplierID, s.CompanyName

-- USE INNER JOIN TO RETRIEVE DATA FROM 2 OTHER TABLES (INDEPENDENT JOINS)
SELECT p.ProductName, p.UnitPrice, s.CompanyName AS "Supplier", c.CategoryName AS "Category"
FROM Products p
INNER JOIN Suppliers s ON p.SupplierID = s.SupplierID
INNER JOIN Categories c ON p.CategoryID = c.CategoryID

-- ANOTHER DOUBLE JOIN EXAMPLE
SELECT o.OrderID, o.OrderDate, o.Freight, c.CompanyName AS "Company Name", e.FirstName + ' ' + e.LastName AS "Employee Name"
FROM Orders o
INNER JOIN Customers c ON o.CustomerID = c.CustomerID
INNER JOIN Employees e ON o.EmployeeID = e.EmployeeID
```
