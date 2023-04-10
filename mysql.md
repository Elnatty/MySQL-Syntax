# Microsoft SQL Server Tutorial

Open the SQL Server Management Studio (SSMS) and login with either windows authentication or Server authentication.
-> you can also login to multiple servers at the same time.

========================================================
SELECT @@SERVERNAME -> to view the db name.
SELECT @@VERSION -> to view the version of the sql server.

===========================================================
Download adventure works database for practice (it has predefined tables for practice/labbing).
===============================================================
SELECT * FROM HumanResources.Department -> select a table to view all content (*) from db.

SELECT DepartmentID, Name FROM HumanResources.Department -> select specific columns from d table.

SELECT DISTINCT Name FROM HumanResources.Department -> select and remove any duplicate value.

SELECT * FROM HumanResources.Department WHERE Name='Production' -> select all items from tablename where columnname='something' (selecting using conditions).

SELECT Name FROM HumanResources.Department WHERE BusinessId > 40 -> select values with conditionals using 'where' and operational values (<, >, <=, >= etc.)

SELECT LoginID, VacationHours, SickLeaveHours, VacationHours + SickLeaveHours AS SumTab FROM HumanResources.Employee -> selecting various columns, then adding them up and displaying their total on a new tab using the 'AS' 'tabname'.

SELECT LoginID, VacationHours, SickLeaveHours, VacationHours / SickLeaveHours AS SumTab FROM HumanResources.Employee WHERE SickLeaveHours > 50 -> when using the division (/) operator, alsway specify a '> 0' or '< 0' in order to avoid errors.

SELECT FirstName,MiddleName,LastName, FirstName + ' ' + MiddleName + ' ' + LastName as FullName from Person.Person -> outputs 'Nathan O Alabi' as full string.

-> or

SELECT FirstName, MiddleName, LastName, CONCAT(FirstName, ' ', MiddleName, ' ', LastName) from Person.Person -> we can use the CONCAT function to add strings.



SELECT FirstName, MiddleName, LastName from Person.Person WHERE MiddleName IS NULL -> outputs FirstName, MiddleName, LastName values where MiddleName is NULL.

SELECT FirstName, MiddleName, LastName from Person.Person WHERE MiddleName IS NOT NULL -> outputs FirstName, MiddleName, LastName values where MiddleName is NOT NULL.

SELECT * FROM HumanResources.Department WHERE Name='Production' AND Age=30 -> select all items from tablename where columnname='something' (selecting using conditions)(you can use 'AND', 'OR' etc.).

SELECT * from Person.Person WHERE BusinessEntityID IN (2,16,20,25,30,1) -> use the 'IN' keyword instead of 'OR' for select query.

SELECT * from Person.Person WHERE BusinessEntityID BETWEEN 1 AND 30 -> the 'BETWEEN' keyword can be used to get a range of values.

SELECT * from Person.Person WHERE FirstName LIKE 'Al%' -> the 'LIKE' keyword is used for matching specific patterns.  % means 0 or more characters.
Outputs name with (Alabi, Alaba, Aliko etc..)
--  > %o -> means 0 or more character before 'o'.

SELECT AddressLine1, City FROM Person.Address ORDER BY City -> sorting items in accending order.

SELECT AddressLine1, City FROM Person.Address ORDER BY City DESC -> sorting items in decending order.

SELECT FirstName, LastName, MiddleName FROM Person.Person WHERE MiddleName IS NOT NULL ORDER BY FirstName -> another example of sorting order.

SELECT SalesOrderID, AVG(UnitPrice) AS AvgUnitPrice FROM Sales.SalesOrderDetail group by SalesOrderID -> calculating average.
	SUM()
	COUNT(), MIN(), MAX()

SELECT FirstName, len(FirstName) as StrLen from Person.Person -> length function.

SELECT FirstName, right(FirstName, 3) as indexingLeft from Person.Personv -> indexing in string using the LEFT or RIGHT function.

SELECT FirstName, SUBSTRING(FirstName, 2, 4) as SubStringFrom3rdTo4thIndex from Person.Person -> using SUBSTRING function to extract from certain ranges of a string.

SELECT SalesOrderID, OrderDate, day(OrderDate) as extractDay from Sales.SalesOrderHeader -> extracting 'DAY(), MONTH(), YEAR()' etc.

select CURRENT_TIMESTAMP -> getting the current time stamp on server PC.


============================================================================================
CREATE DATABASE dbname -> to create a db.
============================================================================================
CREATE TABLE covidStats 
(covidId INT IDENTITY,
 date datetime,
 dailyConfirmedStats INT,
 dailyDeaths smallint,
 country VARCHAR(25),
 covidFlag bit,
 totalLoss money)
-> the 'IDENTITY' denotes autoincrement.
-> can also specify as 'IDENTITY(1,3)' -> meaning autoincrement from 1 to infinity in order of 3's ie; 1,4,7,10 etc.

=============================================================================================
Creating table with constraints.
=============================================================================================
CREATE TABLE itemHeader
(
	itemId INT PRIMARY KEY,
	itemName VARCHAR(25) UNIQUE,
	itemOrderDate DATETIME NOT NULL,
	itemShipDate DATETIME NOT NULL,
	itemAmount MONEY
)
--  > 'NOT NULL' means those columns must have a value
--  > PRIMARY KEY 
--  > UNIQUE to maintain an entity integrity.

=============================================================================================
Inserting into table.
=============================================================================================
INSERT INTO covidStats VALUES ('4/25/2020', 1020, 630, 'US', 1, 304)
or
INSERT INTO covidStats (listAllOrSomeOfTheTableColumns) VALUES (fillTheValues)
or
INSERT INTO covidStats (date, country) VALUES ('1/2/2022', 'Nigeria'), ('10/4/2022', 'Cameroon') -> inserting 2 rows into the table at once.

=============================================================================================Update items in a table.
=============================================================================================
UPDATE covidStats SET column1Name=value, column2Name=value, column3Name=value etc. WHERE condition=?? eg;
UPDATE covidStats SET dailyConfirmedStats=90, dailyDeaths=200, covidFlag=2, totalLoss=500 WHERE covidId=6

=============================================================================================Altering: adding or modifying or deleting a column in a table.
=============================================================================================
ALTER TABLE covidStats ADD continent char(12) -> adding a new column at the end of the table.

ALTER TABLE covidStats ALTER COLUMN continent VARCHAR(12) -> changing the column type to another data type.

ALTER TABLE covidStats DROP COLUMN columnname -> removing a particular colunm

=============================================================================================
Deleting items from a table.
=============================================================================================
DELETE FROM covidStats WHERE country='Nigeria' -> deleting all appearances of Nigeria from the 'country' column in the table.

DELETE FROM covidStats -> deletes the entire items in a table (be careful).
DELETE TOP (2) FROM covidStats -> deletes the top 2 rows in the table.

DROP TABLE covidStats -> deletes the particular table from the db.



============================================================================================================================================================================================
mysql shell tutorials
============================================================================================================================================================================================
CREATE DATABASE dking; -> to create a new database.
SHOW DATABASES; -> to view all databases in GUI mode.
USE dking -> switch to the database.
DESC dking -> shows graphical view of the table in the cmd line.
CREATE SCHEMA `dking_test`; -> to create a new Schema.

--  creating a table 'employee'
CREATE TABLE `dking_test`.`employee` (
  `empId` INT NOT NULL,
  `empName` VARCHAR(60) NOT NULL,
  `empAge` INT NOT NULL,
  `empDept` VARCHAR(45) NOT NULL,
  PRIMARY KEY (`empId`));
  
--  inserting data into the table
INSERT INTO `dking_test`.`employee` (`empId`, `empName`, `empAge`, `empDept`) VALUES ('1', 'Tom', '25', 'Operations');
INSERT INTO `dking_test`.`employee` (`empId`, `empName`, `empAge`, `empDept`) VALUES ('2', 'Emma', '23', 'Finance');
INSERT INTO `dking_test`.`employee` (`empId`, `empName`, `empAge`, `empDept`) VALUES ('3', 'Brad', '27', 'Marketing');
INSERT INTO `dking_test`.`employee` (`empId`, `empName`, `empAge`, `empDept`) VALUES ('4', 'Bradley', '26', 'IT');
INSERT INTO dking_test.employee VALUES ('5', 'Nathan', '22', 'CTO');

-- Check Constraint
CREATE TABLE employee (
  `empId` INT NOT NULL,
  `empName` VARCHAR(60) NOT NULL,
  `empAge` INT NOT NULL,
  `empDept` VARCHAR(45) NOT NULL,
  CHECK(empAge>20)
  );
this means it will check that the value of "empAge" must not be less than 20. If its less, then it throws an error.

-- Default Contstraint
--  this uses the default 'empDept' value as 'Operations' incase no value is passed into it.
CREATE TABLE `dking`.`employee` (
  `empID` INT NOT NULL,
  `name` VARCHAR(45) NOT NULL,
  `empDept` VARCHAR(45) NULL DEFAULT 'Operations');

-- Index Constraint

-- Alter Tables (ie, adding columns to the table)
ALTER TABLE employee ADD empZone VARCHAR(255); -> adds the column 'empZone' to the employee table.

--  Alter Tables (ie. removing a column from the table)
ALTER TABLE employee DROP COLUMN empZone; -> removes the colum from the table.

-- Alter Tables (ie. modifying columns - changing column data types)
ALTER TABLE employee MODIFY COLUMN empDept INT; -> change the 'empDept' data type from 'VARCHAR' to 'INT'.

-- Using the 'WHERE' condition to select items from a table.
-- using the 'AND' operator.
select * from employee where empAge=26 AND empDept='IT';

-- using the 'OR' operator.
select * from employee where empAge=26 OR empDept='IT';

-- Using the 'NOT' Operator.
select * from employee WHERE NOT empAge=27; -> displays all except the row with 'empAge' value of 27.

-- Comments.
SELECT * FROM employee; -- fetch all records in the table.  -> '-- ' is for single line comment.
SELECT * /* */ FROM employee; -- fetch all records in the table.  -> '/* */' is for multi line comment.

-- Count Function (to return the total number of rows matching a specific criteria).
SELECT COUNT(empAge) FROM employee WHERE empAge=25; -> counting number of employees with age 25.
 SELECT COUNT(*) FROM employee;  -> counts the total number of rows in the table 'employee'.

-- Alias (a temporary name given to a table or column while showing results).
SELECT empAge AS age FROM employee; -> we use the 'AS' operator to specify alias value.

-- 'IN'
SELECT * FROM employee WHERE empZone IN('North', 'East'); -- this selects all records with 'North', 'East' IN them.
SELECT * FROM employee WHERE empZone NOT IN('North', 'East'); -- this selects all records that dosen't have 'North', 'East' IN them.


/*
'LIKE operator' searching for a specified pattern in a table.
It has 2 wildcards:
% => zero, one or more characters.
_ => a single character.
*/
SELECT * FROM employee WHERE empName LIKE 'B%'; -- this searches for records starting or ending with 'B' and may have zero, one or more characters.
SELECT * FROM employee WHERE empName LIKE '__m'; -- this searches for records having 2 characters before 'm'.

-- 'BETWEEN' to select records within a given range.
SELECT * FROM employee WHERE empAge BETWEEN 20 AND 25;
SELECT * FROM employee WHERE empAge NOT BETWEEN 20 AND 25;

-- 'CASE' Statement, this goes through conditions and will return a value if the 1st condition is met.
SELECT empName, empDept,
CASE
    WHEN (empAge > 25) THEN 'Employee with eperience, Eligible for Sr. profile.'
    WHEN (empAge = 25) THEN 'Employee is mid-experienced, Eligible!'
    ElSE 'Freshers... new to the company'
END AS Eligibility
FROM employee;

-- DELETE opperator.
DELETE FROM employee WHERE empDept='IT';
DELETE FROM department; -- deletes all the records and columns from the table 'department'.

-- UPDATE operator.
UPDATE employee SET empAge=20 WHERE empID=5;

-- DROP TABLE.
DROP TABLE department;

-- DROP DATABASE.
DROP DATABASE dking;

-- AVG() Function.
SELECT AVG(empAge) FROM employee; -- return the average value of a table column.

-- SUM() Function.
 SELECT SUM(empAge) FROM employee;
 
 -- ORDER BY keyword to sort records in ascending or descending order.
 SELECT* FROM employee ORDER BY empName; -- in alphbetically  accending order.
 SELECT * FROM employee ORDER BY empName DESC; -- in descending order.
 
 -- AUTO INCREMENT
create table student(stdID INT NOT NULL AUTO_INCREMENT, name VARCHAR(255), age INT, PRIMARY KEY(std ID));
INSERT INTO student(name,age) VALUES('Nathan Alabi', 24); -- adds records into the table, which auto increment the stdID value from 1.....n.

-- MAX() Function
SELECT MAX(empAge) AS LargestAge FROM employee; -- fetches the largest age from the table.

-- MIN() Function
SELECT MIN(empAge) AS LargestAge FROM employee; -- fetches the lowest age from the table.

-- Constrains - this specifies rules for data in a table.
NOT NULL -- wont have a null value.
UNIQUE -- all value have unique values.
PRIMARY KEY -- identifies each row in a table eg; Emp ID, SSN No, License No, Student Roll No. etc.
FOREIGN KEY -- uniquely identify a record in a row. used to link 2 tables together, it is a filed in one table that refers to the Primary Key in another Table.
CHECK -- ensures all values in a column satisfies a specific condition eg; Age > 20.
DEFAULT -- set a default value when no value is inserted.
INDEX -- create and retrieve data quickly from a db.

-- JOINS -used to combine 2 or more rows together ie, to join tables which is done based on a related columns.
/*
Types of JOINS
1. Inner Join - this returns results that has matching values in both tables.
2. Left Join - returns all results from the left table and the matched result from the right table.
3 Right Join - returns all results from the right table and the matched reuslt from the left table.
4. Full Join (not supported in mysql)
*/


