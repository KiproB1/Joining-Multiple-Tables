# Joining-Multiple-TablesCREATE DATABASE MyCompany;

USE MyCompany;

CREATE TABLE Employees (
  EmployeeID INT PRIMARY KEY,
  FirstName VARCHAR(255) NOT NULL,
  LastName VARCHAR(255) NOT NULL
);

CREATE TABLE Departments (
  DepartmentID INT PRIMARY KEY,
  DepartmentName VARCHAR(255) NOT NULL
);

CREATE TABLE Salaries (
  EmployeeID INT,
  DepartmentID INT,
  Salary DECIMAL(10,2) NOT NULL,
  FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID),
  FOREIGN KEY (DepartmentID) REFERENCES Departments(DepartmentID)
);
INSERT INTO Employees (FirstName, LastName)
VALUES ('John', 'Doe'),
       ('Jane', 'Smith'),
       ('Alice', 'Johnson'),
       ('Bob', 'Williams'),
       ('Charlie', 'Brown');

INSERT INTO Departments (DepartmentName)
VALUES ('Engineering'),
       ('Marketing'),
       ('Sales');

INSERT INTO Salaries (EmployeeID, DepartmentID, Salary)
VALUES (1, 1, 75000.00),
       (2, 2, 62000.00),
       (3, 3, 90000.00),
       (4, 1, 58000.00);
SELECT e.FirstName, e.LastName, d.DepartmentName
FROM Employees e
LEFT JOIN Salaries s ON e.EmployeeID = s.EmployeeID
LEFT JOIN Departments d ON s.DepartmentID = d.DepartmentID;
SELECT d.DepartmentName, AVG(s.Salary) AS AverageSalary
FROM Departments d
RIGHT JOIN Salaries s ON d.DepartmentID = s.DepartmentID
GROUP BY d.DepartmentID;
SELECT e.FirstName, e.LastName
FROM Employees e
LEFT JOIN Salaries s ON e.EmployeeID = s.EmployeeID
WHERE s.DepartmentID IS NULL;

