Got it! Here is the revised README file:

---

# Employee Company Database Management System

## Introduction

The "EmployeeCompany" database is a comprehensive system designed to manage various aspects of an organization's workforce. It includes tables that capture critical information about employees, departments, job roles, projects, and attendance. The goal of this project is to gain hands-on experience with real-world projects.

## Features

- **Manager:** Stores data about managers including unique ManagerIDs and their corresponding names.
- **Employee:** Holds detailed employee information such as names, gender, date of birth, contact details, age, and their association with managers through the Manager_ID.
- **Department:** Contains information about different organizational units defined by unique DepartmentIDs and descriptive DepartmentNames.
- **JobRole:** Represents various job roles available within the company.
- **JobRole_Department:** Links job roles to departments and tracks employees' tenures in specific roles.
- **Attendance:** Logs employee attendance by date and time.
- **Project:** Records details about ongoing and completed projects within the company.

## Database Schema

Here's the SQL code for creating the database schema:

```sql
-- Creating Manager table
CREATE TABLE Manager (
    ManagerID INT PRIMARY KEY,
    ManagerName VARCHAR(100)
);

-- Creating Employee table
CREATE TABLE Employee (
    EmployeeID INT PRIMARY KEY,
    EmployeeName VARCHAR(100),
    Gender CHAR(1),
    DateOfBirth DATE,
    PhoneNumber VARCHAR(15),
    Email VARCHAR(100),
    Age INT,
    Manager_ID INT,
    FOREIGN KEY (Manager_ID) REFERENCES Manager(ManagerID)
);

-- Creating Department table
CREATE TABLE Department (
    DepartmentID INT PRIMARY KEY,
    DepartmentName VARCHAR(100)
);

-- Creating JobRole table
CREATE TABLE JobRole (
    JobRoleID INT PRIMARY KEY,
    JobRoleName VARCHAR(100)
);

-- Creating JobRole_Department table
CREATE TABLE JobRole_Department (
    JobRoleID INT,
    DepartmentID INT,
    EmployeeID INT,
    StartDate DATE,
    EndDate DATE,
    PRIMARY KEY (JobRoleID, DepartmentID, EmployeeID),
    FOREIGN KEY (JobRoleID) REFERENCES JobRole(JobRoleID),
    FOREIGN KEY (DepartmentID) REFERENCES Department(DepartmentID),
    FOREIGN KEY (EmployeeID) REFERENCES Employee(EmployeeID)
);

-- Creating Attendance table
CREATE TABLE Attendance (
    AttendanceID INT PRIMARY KEY,
    EmployeeID INT,
    Date DATE,
    Time TIME,
    FOREIGN KEY (EmployeeID) REFERENCES Employee(EmployeeID)
);

-- Creating Project table
CREATE TABLE Project (
    ProjectID INT PRIMARY KEY,
    ProjectName VARCHAR(100),
    StartDate DATE,
    EndDate DATE
);
```

## Usage

### Inserting Data

Here are some examples of how to insert data into the tables:

```sql
-- Inserting data into Manager table
INSERT INTO Manager (ManagerID, ManagerName) VALUES (1, 'John Doe');

-- Inserting data into Employee table
INSERT INTO Employee (EmployeeID, EmployeeName, Gender, DateOfBirth, PhoneNumber, Email, Age, Manager_ID)
VALUES (1, 'Jane Smith', 'F', '1990-01-01', '1234567890', 'jane.smith@example.com', 30, 1);

-- Inserting data into Department table
INSERT INTO Department (DepartmentID, DepartmentName) VALUES (1, 'Human Resources');

-- Inserting data into JobRole table
INSERT INTO JobRole (JobRoleID, JobRoleName) VALUES (1, 'Software Engineer');

-- Inserting data into JobRole_Department table
INSERT INTO JobRole_Department (JobRoleID, DepartmentID, EmployeeID, StartDate, EndDate)
VALUES (1, 1, 1, '2022-01-01', NULL);

-- Inserting data into Attendance table
INSERT INTO Attendance (AttendanceID, EmployeeID, Date, Time)
VALUES (1, 1, '2023-01-01', '09:00:00');

-- Inserting data into Project table
INSERT INTO Project (ProjectID, ProjectName, StartDate, EndDate)
VALUES (1, 'Project Alpha', '2022-01-01', '2022-12-31');
```

### Basic Queries

You can query the database to retrieve information. Here are some example queries:

```sql
-- Select all employees
SELECT * FROM Employee;

-- Get all employees managed by a specific manager
SELECT * FROM Employee WHERE Manager_ID = 1;

-- Get all departments
SELECT * FROM Department;

-- Get all job roles in a specific department
SELECT JobRole.JobRoleName
FROM JobRole
JOIN JobRole_Department ON JobRole.JobRoleID = JobRole_Department.JobRoleID
WHERE JobRole_Department.DepartmentID = 1;
```

## Conclusion

This project provides a solid foundation for managing an organization's employee data, allowing you to perform essential operations such as adding, updating, and querying information. It serves as a practical introduction to real-world database management system projects.

---

Feel free to modify this README file according to your needs!
