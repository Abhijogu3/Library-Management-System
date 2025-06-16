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

- Advanced SQL Concepts – Library Management System
==================================================

🔗 JOINS
--------------------------------------------------
1. INNER JOIN – Members with issued books
SELECT m.member_id, m.member_name, b.book_title
FROM members m
INNER JOIN issued_status i ON m.member_id = i.issued_member_id
INNER JOIN books b ON i.issued_book_isbn = b.isbn;

2. LEFT JOIN – All books and their issue info (if any)
SELECT b.book_title, i.issued_date
FROM books b
LEFT JOIN issued_status i ON b.isbn = i.issued_book_isbn;

3. RIGHT JOIN – Employees who issued books
SELECT e.emp_name, i.issued_id
FROM issued_status i
RIGHT JOIN employees e ON e.emp_id = i.issued_emp_id;

4. FULL OUTER JOIN – All issued and non-issued books and employees
SELECT b.book_title, i.issued_id
FROM books b
FULL OUTER JOIN issued_status i ON b.isbn = i.issued_book_isbn;

5. SELF JOIN – Employees managing other employees (hypothetical)
SELECT e1.emp_name AS Manager, e2.emp_name AS Employee
FROM employees e1
JOIN employees e2 ON e1.emp_id = e2.branch_id;

6. CROSS JOIN – Cartesian product of books and branches
SELECT b.book_title, br.branch_address
FROM books b
CROSS JOIN branch br;

7. CROSS APPLY – Simulated example using VALUES
SELECT m.member_id, m.member_name, v.return_reason
FROM members m
CROSS APPLY (VALUES ('Overdue')) AS v(return_reason);

🔎 FILTERING & AGGREGATION
--------------------------------------------------
8. GROUP BY + HAVING
SELECT issued_member_id, COUNT(*) AS total_issued
FROM issued_status
GROUP BY issued_member_id
HAVING COUNT(*) > 2;

9. EXISTS
SELECT * FROM members m
WHERE EXISTS (
    SELECT 1 FROM issued_status i
    WHERE i.issued_member_id = m.member_id
);

10. IN
SELECT book_title FROM books
WHERE isbn IN (
    SELECT issued_book_isbn FROM issued_status
    WHERE issued_emp_id IN ('EMP001', 'EMP002')
);

11. LIKE
SELECT * FROM books WHERE book_title LIKE '%Python%';

12. CASE WHEN
SELECT book_title,
       CASE status
           WHEN 'Issued' THEN 'Currently Borrowed'
           WHEN 'Available' THEN 'In Stock'
           ELSE 'Unknown'
       END AS status_meaning
FROM books;

📂 TEMP TABLES, VARIABLES, CTEs, SUBQUERIES
--------------------------------------------------
13. Table Variable
DECLARE @IssuedBooks TABLE (
    member_id VARCHAR(10),
    book_isbn VARCHAR(50)
);

INSERT INTO @IssuedBooks
SELECT issued_member_id, issued_book_isbn
FROM issued_status;

14. Temp Table
CREATE TABLE #BooksTemp (
    isbn VARCHAR(50),
    title VARCHAR(80)
);
INSERT INTO #BooksTemp
SELECT isbn, book_title FROM books;

15. CTE
WITH BookCounts AS (
    SELECT book_title, COUNT(*) AS total_issued
    FROM issued_status i
    JOIN books b ON i.issued_book_isbn = b.isbn
    GROUP BY book_title
)
SELECT TOP 3 * FROM BookCounts ORDER BY total_issued DESC;

16. Correlated Subquery
SELECT member_name,
       (SELECT MAX(issued_date)
        FROM issued_status i
        WHERE i.issued_member_id = m.member_id) AS last_issued
FROM members m;

🔑 IDENTITY & SCOPE
--------------------------------------------------
17. IDENTITY Column
CREATE TABLE log_activities (
    log_id INT IDENTITY(1,1) PRIMARY KEY,
    description VARCHAR(100)
);

18. SCOPE_IDENTITY
INSERT INTO members (member_id, member_name, member_address, reg_date)
VALUES ('M009', 'New Member', 'XYZ Lane', GETDATE());
SELECT SCOPE_IDENTITY();

🗃️ INDEXING
--------------------------------------------------
19. Clustered Index
CREATE CLUSTERED INDEX idx_books_isbn ON books(isbn);

20. Non-clustered Index
CREATE NONCLUSTERED INDEX idx_books_author ON books(author);

==================================================
END OF FILE
==================================================


- 
