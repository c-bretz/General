# SQL Server Syntax Notes

This document provides a structured overview of SQL Server syntax, including examples of common operations, best practices, and useful functions. It is intended as a quick reference for developers and analysts working with Microsoft SQL Server (T-SQL).

---

## Table of Contents

- Basic Queries
   - DDL - Data Definition Language
   - DML - Data Manipulation Language
   - Joins
   - Subqueries
   - Built-in Functions
   - Indexes
   - Transactions
- Data Types
- Best Practices

---

## Basic Queries

```sql
-- Select all columns
SELECT * FROM Employees;

-- Select specific columns
SELECT FirstName, LastName FROM Employees;

-- Filtering with WHERE
SELECT * FROM Employees WHERE Department = 'HR';

-- Sorting
SELECToyees ORDER BY HireDate DESC;

-- Create a table
CREATE TABLE Departments (
    DepartmentID INT PRIMARY KEY,
    Name NVARCHAR(100) NOT NULL
);

-- Alter a table
ALTER TABLE Employees ADD Salary DECIMAL(10, 2);

-- Drop a table
DROP TABLE TempEmployees;

-- Insert data
INSERT INTO Employees (FirstName, LastName, Department)
VALUES ('John', 'Doe', 'Finance');

-- Update data
UPDATE Employees
SET Department = 'Marketing'
WHERE EmployeeID = 101;

-- Delete data
DELETE FROM Employees WHERE EmployeeID = 101;

-- Inner Join
SELECT e.FirstName, d.Name AS Department
FROM Employees e
INNER JOIN Departments d ON e.DepartmentID = d.DepartmentID;

-- Left Join
SELECT e.FirstName, d.Name AS Department
FROM Employees e
LEFT JOIN Departments d ON e.DepartmentID = d.DepartmentID;

-- Full Outer Join
SELECT e.FirstName, d.Name AS Department
FROM Employees e
FULL OUTER JOIN Departments d ON e.DepartmentID = d.DepartmentID;

-- Subquery in WHERE clause
SELECT FirstName FROM Employees
WHERE DepartmentID IN (
    SELECT DepartmentID FROM Departments WHERE Name = 'IT'
);

-- String functions
SELECT UPPER('sql server'), LEN('text');

-- Date functions
SELECT GETDATE(), DATEADD(DAY, 7, GETDATE());

-- Aggregate functions
SELECT COUNT(*), AVG(Salary), MAX(HireDate) FROM Employees;

-- Create an index
CREATE INDEX idx_lastname ON Employees(LastName);

-- Drop an index
DROP INDEX idx_lastname ON Employees;

BEGIN TRANSACTION;

UPDATE Accounts SET Balance = Balance - 100 WHERE AccountID = 1;
UPDATE Accounts SET Balance = Balance + 100 WHERE AccountID = 2;

-- Commit or Rollback
COMMIT;
-- ROLLBACK;
```

## Data Types
- INT, BIGINT, SMALLINT, TINYINT
- DECIMAL(p, s), NUMERIC(p, s)
- VARCHAR(n), NVARCHAR(n), CHAR(n)
- DATE, DATETIME, SMALLDATETIME, TIME
- BIT (Boolean)
- UNIQUEIDENTIFIER (GUID)

## Best Practices
- Avoid SELECT * in production queries.
- Use TRY_CAST or TRY_CONVERT for safe type conversions.
- Always use transactions for multi-step operations.
- Use WITH (NOLOCK) cautiously to avoid blocking, but be aware of dirty reads
