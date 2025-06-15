# 📘 SQL Server Library Management System

A robust and fully-featured Library Management System using SQL Server. This project demonstrates a wide range of SQL concepts through real-world scenarios like managing books, members, employees, branches, book issuing, and returning.

---

## 🏗️ Features & SQL Concepts Used

### 🔗 Joins
- **INNER JOIN**
- **LEFT JOIN**
- **RIGHT JOIN**
- **FULL OUTER JOIN**
- **SELF JOIN**
- **CROSS JOIN**
- **CROSS APPLY**

### 🔎 Data Filtering & Aggregation
- `GROUP BY`, `HAVING`, `ORDER BY`
- `EXISTS`, `NOT EXISTS`, `IN`, `NOT IN`
- `LIKE`, `NOT LIKE`
- `CASE WHEN` logic

### 📂 Tables & Variables
- Table Variables (`DECLARE @table TABLE`)
- Temp Tables (`CREATE TABLE #Temp`)
- Common Table Expressions (CTEs)
- Subqueries (inline and correlated)

### 🔑 Identity & Scope
- `IDENTITY` columns
- `SCOPE_IDENTITY()`, `@@IDENTITY`

### 🗃️ Indexing
- Clustered Index
- Non-clustered Index

### 🧩 Stored Logic
- **Stored Procedures**
- **Scalar Functions**
- **Table-Valued Functions**
- **Triggers** (`INSERTED`, `DELETED`)
- `OUTPUT` clause

### ⚙️ Error Handling & Transactions
- `TRY...CATCH`
- `RAISERROR`
- `BEGIN TRANSACTION`, `COMMIT`, `ROLLBACK`

### 📊 Advanced SQL
- Ranking Functions: `ROW_NUMBER`, `RANK`, `DENSE_RANK`, `NTILE`
- `PIVOT` and `UNPIVOT`
- Pagination with `OFFSET FETCH`
- `CAST` and `CONVERT`
- `STUFF` function for string manipulation
- XML Parsing
- Dynamic SQL

---

## 🛠️ Technologies Used

- **SQL Server** (T-SQL)
- Microsoft SQL Server Management Studio (SSMS)
- Git for version control

---

## 📁 Project Structure

- `create_tables.sql` - Schema definition
- `insert_data.sql` - Sample data
- `procedures_views_triggers.sql` - Stored procs, functions, triggers
- `queries.sql` - Sample and advanced SQL queries

---
🔗 Joins
1. INNER JOIN
Returns rows when there is a match in both tables.
SELECT Orders.OrderID, Customers.CustomerName
FROM Orders
INNER JOIN Customers ON Orders.CustomerID = Customers.CustomerID;

---
2. LEFT JOIN (LEFT OUTER JOIN)
Returns all rows from the left table, and matched rows from the right table.
SELECT Employees.LastName, Employees.DepartmentID, Departments.DepartmentName
FROM Employees
LEFT JOIN Departments ON Employees.DepartmentID = Departments.DepartmentID;

---
3. RIGHT JOIN (RIGHT OUTER JOIN)
Returns all rows from the right table, and matched rows from the left table.
SELECT Orders.OrderID, Customers.CustomerName
FROM Orders
RIGHT JOIN Customers ON Orders.CustomerID = Customers.CustomerID;

---
4. FULL OUTER JOIN
Returns all rows when there is a match in either left or right table.
SELECT A.Column1, B.Column2
FROM TableA A
FULL JOIN TableB B ON A.Column1 = B.Column2;

---
5. SELF JOIN
Joins a table with itself.
SELECT A.EmployeeID, A.Name, B.Name AS Manager
FROM Employees A, Employees B
WHERE A.ManagerID = B.EmployeeID;

---
6. CROSS JOIN
Returns the Cartesian product of two tables.
server4237.rssing.com
SELECT A.ID, B.ID
FROM TableA A
CROSS JOIN TableB B;

---
7. CROSS APPLY
Applies a table-valued function to each row of the outer table.
SELECT A.ID, B.Value
FROM TableA A
CROSS APPLY dbo.fnGetValues(A.ID) B;
🧾 Grouping & Filtering

--
8. GROUP BY
Groups rows that have the same values into summary rows.
SELECT DepartmentID, COUNT(*) AS NumberOfEmployees
FROM Employees
GROUP BY DepartmentID;

---
9. HAVING
Filters records after GROUP BY.
SELECT DepartmentID, COUNT(*) AS NumberOfEmployees
FROM Employees
GROUP BY DepartmentID
HAVING COUNT(*) > 5;


10. ORDER BY
Sorts the result set.
SELECT * FROM Employees
ORDER BY LastName ASC;


11. EXISTS
Checks for the existence of rows returned by a subquery.
SELECT * FROM Employees E
WHERE EXISTS (
    SELECT 1 FROM Departments D
    WHERE D.DepartmentID = E.DepartmentID
);

--
12. NOT EXISTS
Checks for the non-existence of rows returned by a subquery.
SELECT * FROM Employees E
WHERE NOT EXISTS (
    SELECT 1 FROM Departments D
    WHERE D.DepartmentID = E.DepartmentID
);

---
13. IN
Checks if a value matches any value in a list or subquery.
SELECT * FROM Employees
WHERE DepartmentID IN (1, 2, 3);

---
14. NOT IN
Checks if a value does not match any value in a list or subquery.
SELECT * FROM Employees
WHERE DepartmentID NOT IN (1, 2, 3);

---
15. LIKE
Searches for a specified pattern in a column.
SELECT * FROM Employees
WHERE LastName LIKE 'S%';

---
16. NOT LIKE
Searches for a specified pattern not in a column.
SELECT * FROM Employees
WHERE LastName NOT LIKE 'S%';

---
🗃️ Tables & Variables
17. TABLE VARIABLE
Declares a variable to store a table.
DECLARE @EmployeeTable TABLE (
    EmployeeID INT,
    Name NVARCHAR(100)
);

---
18. TEMP TABLE
Creates a temporary table.
CREATE TABLE #TempEmployees (
    EmployeeID INT,
    Name NVARCHAR(100)
);

---
19. CTE (Common Table Expression)
Defines a temporary result set.
WITH DepartmentCTE AS (
    SELECT DepartmentID, COUNT(*) AS NumberOfEmployees
    FROM Employees
    GROUP BY DepartmentID
)
SELECT * FROM DepartmentCTE;

---
🔑 Identity & Scope
20. IDENTITY KEY
Generates unique numbers for new rows.
dotnetfullstackdev.medium.com
CREATE TABLE Employees (
    EmployeeID INT IDENTITY(1,1),
    Name NVARCHAR(100)
);

---
21. SCOPE_IDENTITY()
Returns the last identity value inserted in the same scope.
INSERT INTO Employees (Name) VALUES ('John Doe');
SELECT SCOPE_IDENTITY();

---
22. @@IDENTITY
Returns the last identity value inserted in the current session.
INSERT INTO Employees (Name) VALUES ('Jane Smith');
SELECT @@IDENTITY;

---
📚 Indexes & Procedures
23. CLUSTERED INDEX
Defines the order of data storage in a table.
CREATE CLUSTERED INDEX idx_EmployeeID
ON Employees (EmployeeID);

---
24. NON-CLUSTERED INDEX
Creates a separate structure from the data table.
CREATE NONCLUSTERED INDEX idx_LastName
ON Employees (LastName);

---
25. STORED PROCEDURE
Encapsulates SQL logic for reuse.
CREATE PROCEDURE GetEmployeeByID (@EmployeeID INT)
AS
BEGIN
    SELECT * FROM Employees WHERE EmployeeID = @EmployeeID;
END;

---
26. SCALAR FUNCTION
Returns a single value.
CREATE FUNCTION dbo.GetFullName (@EmployeeID INT)
RETURNS NVARCHAR(200)
AS
BEGIN
    DECLARE @FullName NVARCHAR(200);
    SELECT @FullName = CONCAT(FirstName, ' ', LastName)
    FROM Employees
    WHERE EmployeeID = @EmployeeID;
    RETURN @FullName;
END;

---
27. TABLE-VALUED FUNCTION
Returns a table.
CREATE FUNCTION dbo.GetEmployeesByDepartment (@DepartmentID INT)
RETURNS TABLE
AS
RETURN (
    SELECT * FROM Employees
    WHERE DepartmentID = @DepartmentID
);

---
28. OUTPUT CLAUSE
Returns inserted or deleted rows.
DECLARE @InsertedRows TABLE (EmployeeID INT, Name NVARCHAR(100));
INSERT INTO Employees (Name)
OUTPUT INSERTED.EmployeeID, INSERTED.Name INTO @InsertedRows
VALUES ('Alice Johnson');
SELECT * FROM @InsertedRows;
---
29. TRY...CATCH
Handles errors in SQL Server.
BEGIN TRY
    -- Code that may cause an error
END TRY
BEGIN CATCH
    -- Error handling code
    SELECT ERROR_MESSAGE();
END CATCH;
---
30. RAISERROR
Generates an error message.
RAISERROR('An error occurred.', 16, 1);
--
32. TRANSACTION
Manages a sequence of operations,
BEGIN TRANSACTION;
COMMIT TRANSACTION;

---
🧮 Conditional Logic & Subqueries
32. CASE WHEN
Evaluates conditions and returns a value.
SELECT Name,
       CASE
           WHEN Salary < 50000 THEN 'Low'
           WHEN Salary BETWEEN 50000 AND 100000 THEN 'Medium'
           ELSE 'High'
       END AS SalaryRange
FROM Employees;

---
33. STUFF
Deletes a specified length of characters and inserts another set of characters.
SELECT STUFF('SQL Server', 5, 0, ' is awesome');

