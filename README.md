## SELECT Syntax
```sql
SELECT * FROM Customers;
```

## SELECT DISTINCT Syntax
return only distinct (different) values.
```sql
SELECT DISTINCT column1, column2, ...
FROM table_name;

SELECT COUNT(DISTINCT Country) FROM Customers;
```

## WHERE Clause
```sql
SELECT * FROM Customers
WHERE CustomerID=1;
```

## SQL AND, OR and NOT Operators
```sql
SELECT * FROM Customers
WHERE Country='Germany' AND (City='Berlin' OR City='München');

SELECT * FROM Customers
WHERE NOT Country='Germany' AND NOT Country='USA';
```

## ORDER BY
selects all customers from the "Customers" table, sorted ascending by the "Country" and descending by the "CustomerName" column:
```sql
SELECT * FROM Customers
ORDER BY Country ASC, CustomerName DESC;
```

## INSERT INTO Syntax
```sql
INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);

INSERT INTO Customers (CustomerName, City, Country)
VALUES ('Cardinal', 'Stavanger', 'Norway');
```

## NULL Value
a field with no value.
```sql
SELECT CustomerName, ContactName, Address
FROM Customers
WHERE Address IS NULL;

SELECT CustomerName, ContactName, Address
FROM Customers
WHERE Address IS NOT NULL;
```

## SQL UPDATE Statement
If you omit the WHERE clause, ALL records will be updated!
```sql
UPDATE Customers
SET ContactName='Juan'
WHERE Country='Mexico';

UPDATE Customers
SET ContactName='Juan';
```

## SQL DELETE Statement
```sql
DELETE FROM Customers WHERE CustomerName='Alfreds Futterkiste';

DELETE FROM table_name;
```

## SQL SELECT TOP
```sql
SELECT TOP 3 * FROM Customers;

SELECT TOP 50 PERCENT * FROM Customers;
```

## SQL MIN() and MAX()
```sql
SELECT MIN(column_name)
FROM table_name
WHERE condition;

SELECT MIN(Price) AS SmallestPrice
FROM Products;

SELECT MAX(column_name)
FROM table_name
WHERE condition;

SELECT MAX(Price) AS LargestPrice
FROM Products;
```

## SQL COUNT(), AVG() and SUM()
```sql
SELECT COUNT(ProductID)
FROM Products;

SELECT AVG(Price)
FROM Products;

SELECT SUM(Quantity)
FROM OrderDetails;
```

## SQL LIKE Operator
The percent sign (%) represents zero, one, or multiple characters
The underscore sign (_) represents one, single character
```sql
WHERE CustomerName LIKE 'a%'	=> Finds any values that start with "a"
WHERE CustomerName LIKE '%a'	=> Finds any values that end with "a"
WHERE CustomerName LIKE '%or%'	=> Finds any values that have "or" in any position
WHERE CustomerName LIKE '_r%'	=> Finds any values that have "r" in the second position
WHERE CustomerName LIKE 'a_%'	=> Finds any values that start with "a" and are at least 2 characters in length
WHERE CustomerName LIKE 'a__%'	=> Finds any values that start with "a" and are at least 3 characters in length
WHERE ContactName LIKE 'a%o'	=> Finds any values that start with "a" and ends with "o"

--The following SQL statement selects all customers with a CustomerName that does NOT start with "a":
SELECT * FROM Customers
WHERE CustomerName NOT LIKE 'a%';
```

## SQL Wildcard Characters
A wildcard character is used to substitute one or more characters in a string.
```sql

Symbol	Description	                    Example
%	Represents zero or more characters => bl% finds bl, black, blue, and blob
_	Represents a single character	 => h_t finds hot, hat, and hit
[]	Represents any single character within the brackets	 => h[oa]t finds hot and hat, but not hit
^	Represents any character not in the brackets	 => h[^oa]t finds hit, but not hot and hat
-	Represents any single character within the specified range => c[a-b]t finds cat and cbt
 
WHERE CustomerName LIKE 'a%' => Finds any values that starts with "a"
WHERE CustomerName LIKE '%a' => Finds any values that ends with "a"
WHERE CustomerName LIKE '%or%' => Finds any values that have "or" in any position
WHERE CustomerName LIKE '_r%' => Finds any values that have "r" in the second position
WHERE CustomerName LIKE 'a__%' => Finds any values that starts with "a" and are at least 3 characters in length
WHERE ContactName LIKE 'a%o' => Finds any values that starts with "a" and ends with "o"

SELECT * FROM Customers
WHERE City NOT LIKE '[bsp]%';
```

## SQL IN Operator
```sql
SELECT column_name(s)
FROM table_name
WHERE column_name IN (SELECT STATEMENT);

SELECT * FROM Customers
WHERE Country NOT IN ('Germany', 'France', 'UK');

SELECT * FROM Customers
WHERE Country IN (SELECT Country FROM Suppliers);
```

## SQL BETWEEN Operator
The values can be numbers, text, or dates.
```sql
SELECT * FROM Products
WHERE Price BETWEEN 10 AND 20;

SELECT * FROM Products
WHERE Price NOT BETWEEN 10 AND 20;

SELECT * FROM Products
WHERE Price BETWEEN 10 AND 20
AND CategoryID NOT IN (1,2,3);

SELECT * FROM Products
WHERE ProductName BETWEEN "Carnarvon Tigers" AND "Chef Anton's Cajun Seasoning"
ORDER BY ProductName;

SELECT * FROM Orders
WHERE OrderDate BETWEEN '1996-07-01' AND '1996-07-31';
```

## SQL Aliases
```sql
SELECT column_name AS alias_name
FROM table_name;

SELECT column_name(s)
FROM table_name AS alias_name;

SELECT CustomerName AS Customer, ContactName AS [Contact Person]
FROM Customers;

SELECT CustomerName, Address + ', ' + PostalCode + ' ' + City + ', ' + Country AS Address
FROM Customers;

SELECT o.OrderID, o.OrderDate, c.CustomerName
FROM Customers AS c, Orders AS o
WHERE c.CustomerName='Around the Horn' AND c.CustomerID=o.CustomerID;

SELECT Orders.OrderID, Orders.OrderDate, Customers.CustomerName
FROM Customers, Orders
WHERE Customers.CustomerName='Around the Horn' AND Customers.CustomerID=Orders.CustomerID;
```

## SQL JOIN
A JOIN clause is used to combine rows from two or more tables, based on a related column between them.
```sql 
SELECT Orders.OrderID, Customers.CustomerName, Orders.OrderDate
FROM Orders
INNER JOIN Customers ON Orders.CustomerID=Customers.CustomerID;

SELECT Orders.OrderID, Customers.CustomerName, Shippers.ShipperName
FROM ((Orders
INNER JOIN Customers ON Orders.CustomerID = Customers.CustomerID)
INNER JOIN Shippers ON Orders.ShipperID = Shippers.ShipperID);

SELECT Customers.CustomerName, Orders.OrderID
FROM Customers
LEFT JOIN Orders ON Customers.CustomerID = Orders.CustomerID
ORDER BY Customers.CustomerName;

SELECT column_name(s)
FROM table1
RIGHT JOIN table2
ON table1.column_name = table2.column_name;

SELECT Orders.OrderID, Employees.LastName, Employees.FirstName
FROM Orders
RIGHT JOIN Employees ON Orders.EmployeeID = Employees.EmployeeID
ORDER BY Orders.OrderID;

SELECT column_name(s)
FROM table1
FULL OUTER JOIN table2
ON table1.column_name = table2.column_name
WHERE condition;

SELECT Customers.CustomerName, Orders.OrderID
FROM Customers
FULL OUTER JOIN Orders ON Customers.CustomerID=Orders.CustomerID
ORDER BY Customers.CustomerName;

SELECT column_name(s)
FROM table1 T1, table1 T2
WHERE condition;

SELECT A.CustomerName AS CustomerName1, B.CustomerName AS CustomerName2, A.City
FROM Customers A, Customers B
WHERE A.CustomerID <> B.CustomerID
AND A.City = B.City
ORDER BY A.City;
```

## SQL UNION Operator
combine the result-set of two or more SELECT statements.
```sql
SELECT City FROM Customers
UNION
SELECT City FROM Suppliers
ORDER BY City;

SELECT City FROM Customers
UNION ALL
SELECT City FROM Suppliers
ORDER BY City;
```

## SQL GROUP BY Statement
The GROUP BY statement groups rows that have the same values into summary rows, like "find the number of customers in each country".
```sql
SELECT column_name(s)
FROM table_name
WHERE condition
GROUP BY column_name(s)
ORDER BY column_name(s);

SELECT COUNT(CustomerID), Country
FROM Customers
GROUP BY Country;

SELECT COUNT(CustomerID), Country
FROM Customers
GROUP BY Country
ORDER BY COUNT(CustomerID) DESC;

SELECT Shippers.ShipperName, COUNT(Orders.OrderID) AS NumberOfOrders FROM Orders
LEFT JOIN Shippers ON Orders.ShipperID = Shippers.ShipperID
GROUP BY ShipperName;
```

## SQL HAVING Clause
The HAVING clause was added to SQL because the WHERE keyword cannot be used with aggregate functions.
```sql
SELECT column_name(s)
FROM table_name
WHERE condition
GROUP BY column_name(s)
HAVING condition
ORDER BY column_name(s);

SELECT COUNT(CustomerID), Country
FROM Customers
GROUP BY Country
HAVING COUNT(CustomerID) > 5
ORDER BY COUNT(CustomerID) DESC;

SELECT Employees.LastName, COUNT(Orders.OrderID) AS NumberOfOrders
FROM (Orders
INNER JOIN Employees ON Orders.EmployeeID = Employees.EmployeeID)
GROUP BY LastName
HAVING COUNT(Orders.OrderID) > 10;

SELECT Employees.LastName, COUNT(Orders.OrderID) AS NumberOfOrders
FROM Orders
INNER JOIN Employees ON Orders.EmployeeID = Employees.EmployeeID
WHERE LastName = 'Davolio' OR LastName = 'Fuller'
GROUP BY LastName
HAVING COUNT(Orders.OrderID) > 25;
```

## SQL EXISTS Operator
The EXISTS operator is used to test for the existence of any record in a subquery.
The EXISTS operator returns TRUE if the subquery returns one or more records.
```sql
SELECT column_name(s)
FROM table_name
WHERE EXISTS
(SELECT column_name FROM table_name WHERE condition);

SELECT SupplierName
FROM Suppliers
WHERE EXISTS (SELECT ProductName FROM Products WHERE Products.SupplierID = Suppliers.supplierID AND Price < 20);

SELECT SupplierName
FROM Suppliers
WHERE EXISTS (SELECT ProductName FROM Products WHERE Products.SupplierID = Suppliers.supplierID AND Price = 22);

```

## SQL ANY and ALL Operators
returns TRUE if ANY of the subquery values meet the condition
returns TRUE if ALL of the subquery values meet the condition
```sql
SELECT column_name(s)
FROM table_name
WHERE column_name operator ANY
  (SELECT column_name
  FROM table_name
  WHERE condition);
  
SELECT ProductName
FROM Products
WHERE ProductID = ANY
  (SELECT ProductID
  FROM OrderDetails
  WHERE Quantity = 10);
  
SELECT ProductName
FROM Products
WHERE ProductID = ANY
  (SELECT ProductID
  FROM OrderDetails
  WHERE Quantity > 99);
  
SELECT ProductName
FROM Products
WHERE ProductID = ANY
  (SELECT ProductID
  FROM OrderDetails
  WHERE Quantity > 1000);
  
SELECT column_name(s)
FROM table_name
WHERE column_name operator ALL
  (SELECT column_name
  FROM table_name
  WHERE condition);
  
SELECT ProductName
FROM Products
WHERE ProductID = ALL
  (SELECT ProductID
  FROM OrderDetails
  WHERE Quantity = 10);
```

## SQL SELECT INTO Statement
The SELECT INTO statement copies data from one table into a new table.
```sql
SELECT *
INTO newtable [IN externaldb]
FROM oldtable
WHERE condition;

SELECT * INTO CustomersGermany
FROM Customers
WHERE Country = 'Germany';

SELECT Customers.CustomerName, Orders.OrderID
INTO CustomersOrderBackup2017
FROM Customers
LEFT JOIN Orders ON Customers.CustomerID = Orders.CustomerID;

SELECT * INTO newtable
FROM oldtable
WHERE 1 = 0;
```

## The SQL INSERT INTO SELECT Statement
The INSERT INTO SELECT statement copies data from one table and inserts it into another table.
The INSERT INTO SELECT statement requires that the data types in source and target tables match.
```sql
INSERT INTO table2 (column1, column2, column3, ...)
SELECT column1, column2, column3, ...
FROM table1
WHERE condition;

INSERT INTO Customers (CustomerName, City, Country)
SELECT SupplierName, City, Country FROM Suppliers
WHERE Country='Germany';
```

## SQL CASE Expression
If there is no ELSE part and no conditions are true, it returns NULL.
```sql
CASE
    WHEN condition1 THEN result1
    WHEN condition2 THEN result2
    WHEN conditionN THEN resultN
    ELSE result
END;

SELECT OrderID, Quantity,
CASE
    WHEN Quantity > 30 THEN 'The quantity is greater than 30'
    WHEN Quantity = 30 THEN 'The quantity is 30'
    ELSE 'The quantity is under 30'
END AS QuantityText
FROM OrderDetails;

SELECT CustomerName, City, Country
FROM Customers
ORDER BY
(CASE
    WHEN City IS NULL THEN Country
    ELSE City
END);
```

## SQL NULL Functions
The SQL Server ISNULL() function lets you return an alternative value when an expression is NULL:

```sql
SELECT ProductName, UnitPrice * (UnitsInStock + ISNULL(UnitsOnOrder, 0))
FROM Products;

SELECT ProductName, UnitPrice * (UnitsInStock + COALESCE(UnitsOnOrder, 0))
FROM Products;
```

## SQL Stored Procedures
can save, so the code can be reused over and over again.
pass parameters to a stored procedure, so that the stored procedure can act based on the parameter value(s) that is passed.
```sql
CREATE PROCEDURE procedure_name
AS
sql_statement
GO;
EXEC procedure_name;

CREATE PROCEDURE SelectAllCustomers
AS
SELECT * FROM Customers
GO;
EXEC SelectAllCustomers;

CREATE PROCEDURE SelectAllCustomers @City nvarchar(30)
AS
SELECT * FROM Customers WHERE City = @City
GO;
EXEC SelectAllCustomers @City = 'London';

CREATE PROCEDURE SelectAllCustomers @City nvarchar(30), @PostalCode nvarchar(10)
AS
SELECT * FROM Customers WHERE City = @City AND PostalCode = @PostalCode
GO;
EXEC SelectAllCustomers @City = 'London', @PostalCode = 'WA1 1DP';
```

## SQL Comments
```sql
--SELECT * FROM Customers;
SELECT * FROM Products;
SELECT CustomerName, /*City,*/ Country FROM Customers;
```

## SQL Operators
```sql
Operator	Description	Example
ALL => TRUE if all of the subquery values meet the condition	
AND => TRUE if all the conditions separated by AND is TRUE	
ANY => TRUE if any of the subquery values meet the condition	
BETWEEN => TRUE if the operand is within the range of comparisons	
EXISTS => TRUE if the subquery returns one or more records	
IN => TRUE if the operand is equal to one of a list of expressions	
LIKE => TRUE if the operand matches a pattern	
NOT => Displays a record if the condition(s) is NOT TRUE	
OR => TRUE if any of the conditions separated by OR is TRUE	
SOME => TRUE if any of the subquery values meet the condition
```

## SQL CREATE TABLE Statement
```sql
CREATE TABLE Persons (
    PersonID int,
    LastName varchar(255),
    FirstName varchar(255),
    Address varchar(255),
    City varchar(255)
);

CREATE TABLE TestTable AS
SELECT customername, contactname
FROM customers;
```

## SQL DROP TABLE Statement
The TRUNCATE TABLE statement is used to delete the data inside a table, but not the table itself.
```sql
DROP TABLE Shippers;
TRUNCATE TABLE table_name;
```

## SQL ALTER TABLE Statement
The ALTER TABLE statement is used to add, delete, or modify columns in an existing table.
The ALTER TABLE statement is also used to add and drop various constraints on an existing table.
```sql
ALTER TABLE Customers
ADD Email varchar(255);

ALTER TABLE Customers
DROP COLUMN Email;

ALTER TABLE table_name
RENAME COLUMN old_name to new_name;

ALTER TABLE table_name
ALTER COLUMN column_name datatype;

ALTER TABLE Persons
ALTER COLUMN DateOfBirth year;

ALTER TABLE Persons
DROP COLUMN DateOfBirth;
```

## SQL NOT NULL Constraint
```sql 
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255) NOT NULL,
    Age int
);

ALTER TABLE Persons
ALTER COLUMN Age int NOT NULL;
```

## SQL UNIQUE Constraint
The UNIQUE constraint ensures that all values in a column are different.
A PRIMARY KEY constraint automatically has a UNIQUE constraint.
However, you can have many UNIQUE constraints per table, but only one PRIMARY KEY constraint per table.
```sql
CREATE TABLE Persons (
    ID int NOT NULL UNIQUE,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int
);

CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int,
    CONSTRAINT UC_Person UNIQUE (ID,LastName)
);

ALTER TABLE Persons
ADD UNIQUE (ID);

ALTER TABLE Persons
ADD CONSTRAINT UC_Person UNIQUE (ID,LastName);

ALTER TABLE Persons
DROP CONSTRAINT UC_Person;
```

## SQL PRIMARY KEY Constraint
```sql
CREATE TABLE Persons (
    ID int NOT NULL PRIMARY KEY,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int
);

CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int,
    CONSTRAINT PK_Person PRIMARY KEY (ID,LastName)
);

ALTER TABLE Persons
ADD PRIMARY KEY (ID);

ALTER TABLE Persons
ADD CONSTRAINT PK_Person PRIMARY KEY (ID,LastName);

ALTER TABLE Persons
DROP CONSTRAINT PK_Person;
```

## SQL FOREIGN KEY Constraint
A FOREIGN KEY is a field (or collection of fields) in one table, that refers to the PRIMARY KEY in another table.
```sql
CREATE TABLE Orders (
    OrderID int NOT NULL PRIMARY KEY,
    OrderNumber int NOT NULL,
    PersonID int FOREIGN KEY REFERENCES Persons(PersonID)
);

CREATE TABLE Orders (
    OrderID int NOT NULL,
    OrderNumber int NOT NULL,
    PersonID int,
    PRIMARY KEY (OrderID),
    CONSTRAINT FK_PersonOrder FOREIGN KEY (PersonID)
    REFERENCES Persons(PersonID)
);

ALTER TABLE Orders
ADD FOREIGN KEY (PersonID) REFERENCES Persons(PersonID);

ALTER TABLE Orders
ADD CONSTRAINT FK_PersonOrder
FOREIGN KEY (PersonID) REFERENCES Persons(PersonID);

ALTER TABLE Orders
DROP CONSTRAINT FK_PersonOrder;
```

## SQL CHECK Constraint
The CHECK constraint is used to limit the value range that can be placed in a column.
```sql
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int CHECK (Age>=18)
);

CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int,
    City varchar(255),
    CONSTRAINT CHK_Person CHECK (Age>=18 AND City='Sandnes')
);

ALTER TABLE Persons
ADD CHECK (Age>=18);

ALTER TABLE Persons
ADD CONSTRAINT CHK_PersonAge CHECK (Age>=18 AND City='Sandnes');

ALTER TABLE Persons
DROP CONSTRAINT CHK_PersonAge;
```

## SQL DEFAULT Constraint
```sql 
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int,
    City varchar(255) DEFAULT 'Sandnes'
);

CREATE TABLE Orders (
    ID int NOT NULL,
    OrderNumber int NOT NULL,
    OrderDate date DEFAULT GETDATE()
);

ALTER TABLE Persons
ADD CONSTRAINT df_City
DEFAULT 'Sandnes' FOR City;

ALTER TABLE Persons
ALTER COLUMN City DROP DEFAULT;
```

## SQL CREATE INDEX Statement
```sql
CREATE INDEX index_name
ON table_name (column1, column2, ...);

CREATE INDEX idx_pname
ON Persons (LastName, FirstName);

DROP INDEX table_name.index_name;
```

## SQL AUTO INCREMENT Field
 To specify that the "Personid" column should start at value 10 and increment by 5, change it to IDENTITY(10,5).
```sql
CREATE TABLE Persons (
    Personid int IDENTITY(1,1) PRIMARY KEY,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int
);
```

## SQL Dates
SQL Server comes with the following data types for storing a date or a date/time value in the database:
```sql
DATE - format YYYY-MM-DD
DATETIME - format: YYYY-MM-DD HH:MI:SS
SMALLDATETIME - format: YYYY-MM-DD HH:MI:SS
TIMESTAMP - format: a unique number
```

## SQL Views

```sql
CREATE VIEW [Brazil Customers] AS
SELECT CustomerName, ContactName
FROM Customers
WHERE Country = 'Brazil';

SELECT * FROM [Brazil Customers];

CREATE VIEW [Products Above Average Price] AS
SELECT ProductName, Price
FROM Products
WHERE Price > (SELECT AVG(Price) FROM Products);

SELECT * FROM [Products Above Average Price];


CREATE OR REPLACE VIEW [Brazil Customers] AS
SELECT CustomerName, ContactName, City
FROM Customers
WHERE Country = 'Brazil';

DROP VIEW [Brazil Customers];
```

##
```sql

```

##
```sql

```

##
```sql

```

##
```sql

```

##
```sql
 
```

##
```sql

```

##
```sql

```

##
```sql

```

##
```sql

```

##
```sql

```

##
```sql

```

##
```sql

```

##
```sql

```

##
```sql

```

##
```sql

```

##
```sql

```

##
```sql

```

##
```sql

```

##
```sql

```

##
```sql

```

##
```sql
 
```

