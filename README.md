Question:  11  i)

CREATE TABLE EmployeeProjects (
EmployeeID INT,
EmployeeName VARCHAR(50),
ProjectName VARCHAR(50)
);

INSERT INTO EmployeeProjects  VALUES (101, 'Alice', 'ProjectA');
INSERT INTO EmployeeProjects  VALUES (101, 'Alice', 'ProjectB');
INSERT INTO EmployeeProjects  VALUES (101, 'Alice', 'ProjectC');
INSERT INTO EmployeeProjects  VALUES (102, 'Bob', 'ProjectD');
INSERT INTO EmployeeProjects  VALUES (103, 'Charlie', 'ProjectE');
INSERT INTO EmployeeProjects  VALUES (103, 'Charlie', 'ProjectF');
INSERT INTO EmployeeProjects  VALUES (104, 'David', 'ProjectG');
INSERT INTO EmployeeProjects  VALUES (104, 'David', 'ProjectH');
INSERT INTO EmployeeProjects  VALUES (104, 'David', 'ProjectI');
INSERT INTO EmployeeProjects  VALUES (104, 'David', 'ProjectJ');

select * from EmployeeProjects;

Question 11 ii)

CREATE TABLE Orders (
OrderID INT,
CustomerName VARCHAR(50),
OrderDate DATE,
TotalAmount DECIMAL(10, 2)
);

CREATE TABLE OrderItems (
OrderID INT,
ItemName VARCHAR(50)
);


INSERT INTO Orders VALUES (1, 'Alice', '2024-04-01', 250.00);
INSERT INTO Orders VALUES (2, 'Bob', '2024-04-02', 100.00);
INSERT INTO Orders VALUES (3, 'Charlie', '2024-04-03', 60.00);


INSERT INTO OrderItems VALUES (1, 'Book');
INSERT INTO OrderItems VALUES (1, 'Notebook');
INSERT INTO OrderItems VALUES (1, 'Pen');
INSERT INTO OrderItems VALUES (2, 'Eraser');
INSERT INTO OrderItems VALUES (2, 'Pencil');
INSERT INTO OrderItems VALUES (3, 'Diary');


SELECT
o.OrderID,
o.CustomerName,
o.OrderDate,
GROUP_CONCAT(oi.ItemName ORDER BY oi.ItemName SEPARATOR ',') AS Items,
o.TotalAmount
FROM
Orders o
JOIN
OrderItems oi ON o.OrderID = oi.OrderID
GROUP BY
o.OrderID, o.CustomerName, o.OrderDate, o.TotalAmount;

14. i)

CREATE TABLE Customer (
CustomerID INT PRIMARY KEY,
CustomerName VARCHAR(50)
);

CREATE TABLE Products (
ProductID INT PRIMARY KEY,
ProductName VARCHAR(50),
Category VARCHAR(50),
Price DECIMAL(10,2)
);

CREATE TABLE Orders (
OrderID INT PRIMARY KEY,
CustomerID INT,
ProductID INT,
Quantity INT,
Amount DECIMAL(10,2),
FOREIGN KEY (CustomerID) REFERENCES Customer(CustomerID),
FOREIGN KEY (ProductID) REFERENCES Products(ProductID)
);


INSERT INTO Customer VALUES
(1, 'Alice Smith'),
(2, 'Bob Johnson'),
(3, 'Charlie Brown'),
(4, 'Diana Lee'),
(5, 'Eve Williams');

INSERT INTO Products VALUES
(1, 'Laptop', 'Electronics', 1200.00),
(2, 'Mouse', 'Electronics', 20.00),
(3, 'Keyboard', 'Electronics', 50.00),
(4, 'Shirt', 'Apparel', 75.00),
(5, 'Cushion', 'Home Goods', 50.00);

INSERT INTO Orders VALUES
(101, 1, 1, 1, 1200.00),
(102, 1, 2, 2, 40.00),
(103, 1, 3, 1, 50.00),
(104, 2, 2, 1, 20.00),
(105, 3, 1, 1, 1200.00),
(106, 3, 2, 1, 20.00),
(107, 3, 3, 1, 50.00),
(108, 2, 2, 1, 20.00),
(109, 1, 2, 1, 20.00);

SELECT
c.CustomerName,
SUM(o.Amount) AS TotalAmountSpent
FROM
Customer c
JOIN
Orders o ON c.CustomerID = o.CustomerID
GROUP BY
c.CustomerName;

SELECT p.ProductName,
COUNT(*) AS TotalUnitsSold
FROM Orders o
JOIN Products p ON o.ProductID = p.ProductID
GROUP BY p.ProductName
ORDER BY TotalUnitsSold DESC
LIMIT 1;

SELECT c.CustomerName FROM Customer c
LEFT JOIN
Orders o ON c.CustomerID = o.CustomerID
WHERE o.OrderID IS NULL;

SELECT Category,
MAX(Price) AS MostExpensivePrice
FROM Products GROUP BY Category;




Question 16 i)


CREATE TABLE Admissions (
    admission_id INT PRIMARY KEY,
    patient_name VARCHAR(50),
    department VARCHAR(50),
    stay_days INT
);


INSERT INTO Admissions VALUES
(1, 'Alice Smith', 'Cardiology', 5),
(2, 'Alice Smith', 'Neurology', 4),
(3, 'Bob Johnson', 'Cardiology', 3),
(4, 'Bob Johnson', 'Neurology', 2),
(5, 'Charlie Rose', 'Orthopedics', 7),
(6, 'Diana King', 'Cardiology', 6),
(7, 'Evan Lee', 'Neurology', 2);


SELECT patient_name FROM Admissions
WHERE department = 'Cardiology'
INTERSECT
SELECT patient_name FROM Admissions
WHERE department = 'Neurology';


SELECT COUNT(*) AS TotalAdmissions FROM Admissions;

SELECT
    MAX(stay_days) AS LongestStayDays,
    MIN(stay_days) AS ShortestStayDays
FROM Admissions;


Question 17  i)


CREATE TABLE EmployeePayroll (
    EmployeeID INT PRIMARY KEY,
    EmployeeName VARCHAR(50),
    BaseSalary DECIMAL(10,2),
    Bonus DECIMAL(10,2)
);


INSERT INTO EmployeePayroll VALUES
(101, 'John Doe', 50000.00, 5000.00),
(102, 'Emily Clark', 60000.00, 7000.00),
(103, 'Michael Lee', 55000.00, 4000.00),
(104, 'Sarah Adams', 48000.00, 6000.00),
(105, 'David Wilson', 62000.00, 8000.00);


CREATE VIEW PayrollSummary AS
SELECT
    EmployeeID,
    EmployeeName,
    BaseSalary,
    Bonus,
    (BaseSalary + Bonus) AS TotalSalary
FROM EmployeePayroll;


SELECT * FROM PayrollSummary;


Question 17 ii)


CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerID INT,
    TotalAmount DECIMAL(10,2)
);


INSERT INTO Orders VALUES
(201, 1001, 500.00),
(202, 1002, 1200.50),
(203, 1003, 750.75),
(204, 1004, 980.00),
(205, 1005, 1500.00);


CREATE VIEW OrderSummary AS
SELECT
    OrderID,
    CustomerID,
    TotalAmount,
    (TotalAmount * 0.10) AS TaxAmount
FROM Orders;


SELECT * FROM OrderSummary;

Question 19  i)


CREATE TABLE Employees (
    emp_id INT PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    email VARCHAR(100)
);


INSERT INTO Employees VALUES
(1, 'John', 'Doe', 'john.doe@company.com'),
(2, 'Jane', 'Smith', 'jane.smith@company.com'),
(3, 'Peter', 'Jones', 'peter.jones@company.com'),
(4, 'Mary', 'Brown', 'mary.brown@company.com');


SELECT
    emp_id,
    first_name,
    last_name,
    email,
    SUBSTRING(email, LOCATE('@', email) + 1) AS domain_name
FROM Employees;



Question 19 ii)

CREATE TABLE Customers (
    customer_id INT PRIMARY KEY,
    name VARCHAR(50),
    address VARCHAR(100)
);
INSERT INTO Customers VALUES
(1, 'Alice Smith', '123 Main St, Anytown, CA, 91234'),
(2, 'Bob Johnson', '456 Oak Ave, Springfield, IL, 62704'),
(3, 'Charlie Brown', '789 Pine Ln, Pleasantville, NY, 10570'),
(4, 'Diana Lee', '101 Elm Rd, Anytown, CA, 91234');
SELECT
    customer_id,
    name,
    address,
    SUBSTRING(
        address,
        LOCATE(',', address) + 2,
      LOCATE(',', address, LOCATE(',', address) + 1) - LOCATE(',', address) - 2
    ) AS city
FROM Customers;
