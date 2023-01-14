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

