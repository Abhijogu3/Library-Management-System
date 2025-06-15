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
