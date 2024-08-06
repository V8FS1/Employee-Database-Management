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
REATE SCHEMA IF NOT EXISTS `EmployeeCompany` DEFAULT CHARACTER SET utf8;
USE `EmployeeCompany`;

CREATE TABLE IF NOT EXISTS `EmployeeCompany`.`Maneger` (
    `ManagerID` INT(5) NOT NULL,
    `ManegeName` VARCHAR(45) NOT NULL,
    PRIMARY KEY (`ManagerID`)
) ENGINE = InnoDB;

CREATE TABLE IF NOT EXISTS `EmployeeCompany`.`Employee` (
    `EM_ID` INT(5) NOT NULL,
    `FirstName` VARCHAR(45) NOT NULL,
    `LastName` VARCHAR(45) NOT NULL,
    `Gender` VARCHAR(45) NOT NULL,
    `DateOfBirth` DATE NOT NULL,
    `Phone` INT(10) NULL,
    `Email` VARCHAR(45) NULL,
    `Age` INT(2) NOT NULL,
    `Maneger_ID` INT(5) NULL,
    PRIMARY KEY (`EM_ID`),
    CONSTRAINT `fk_Employee_Maneger1`
    FOREIGN KEY (`Maneger_ID`)
    REFERENCES `EmployeeCompany`.`Maneger` (`ManagerID`)
    ON DELETE SET NULL
    ON UPDATE CASCADE
) ENGINE = InnoDB;

CREATE TABLE IF NOT EXISTS `EmployeeCompany`.`Department` (
    `DepartmentID` VARCHAR(5) NOT NULL,
    `DepartmentName` VARCHAR(255) NOT NULL,
    PRIMARY KEY (`DepartmentID`)
) ENGINE = InnoDB;

CREATE TABLE IF NOT EXISTS `EmployeeCompany`.`JobRole` (
    `JobName` VARCHAR(45) NOT NULL,
    PRIMARY KEY (`JobName`)
) ENGINE = InnoDB;

CREATE TABLE IF NOT EXISTS `EmployeeCompany`.`JobRole_Department` (
    `JobRoleDepartmentID` INT(5) NOT NULL,
    `JobRole_JobName` VARCHAR(45) NOT NULL,
    `Department_ID` VARCHAR(5) NOT NULL,
    `Employee_idEmployee` INT(5) NOT NULL,
    `StartDate` DATE NOT NULL,
    `EndDate` DATE NOT NULL,
    PRIMARY KEY (`JobRoleDepartmentID`, `JobRole_JobName`, `Department_ID`, `Employee_idEmployee`),
    CONSTRAINT `fk_EmployeeDepartment_JobRole1`
    FOREIGN KEY (`JobRole_JobName`)
    REFERENCES `EmployeeCompany`.`JobRole` (`JobName`)
    ON DELETE CASCADE
    ON UPDATE CASCADE,
    CONSTRAINT `fk_EmployeeDepartment_Department1`
    FOREIGN KEY (`Department_ID`)
    REFERENCES `EmployeeCompany`.`Department` (`DepartmentID`)
    ON DELETE CASCADE
    ON UPDATE CASCADE,
    CONSTRAINT `fk_EmployeeDepartment_Employee1`
    FOREIGN KEY (`Employee_idEmployee`)
    REFERENCES `EmployeeCompany`.`Employee` (`EM_ID`)
    ON DELETE CASCADE
    ON UPDATE CASCADE
) ENGINE = InnoDB;

CREATE TABLE IF NOT EXISTS `EmployeeCompany`.`Attandance` (
    `AID` INT(5) NOT NULL,
    `Date` DATE NOT NULL,
    `ClockInTime` VARCHAR(45) NOT NULL,
    `ClockOutTime` VARCHAR(45) NOT NULL,
    `Employee_idEmployee` INT(10) NOT NULL,
    PRIMARY KEY (`AID`, `Employee_idEmployee`),
    CONSTRAINT `fk_Attandance_Employee1`
    FOREIGN KEY (`Employee_idEmployee`)
    REFERENCES `EmployeeCompany`.`Employee` (`EM_ID`)
    ON DELETE CASCADE
    ON UPDATE CASCADE
) ENGINE = InnoDB;

CREATE TABLE IF NOT EXISTS `EmployeeCompany`.`Project` (
    `ProjectName` VARCHAR(45) NOT NULL,
    `ProjectStartDate` DATE NOT NULL,
    `ProjectEndDate` DATE NULL,
    PRIMARY KEY (`ProjectName`)
) ENGINE = InnoDB;

CREATE TABLE IF NOT EXISTS `EmployeeCompany`.`ProjectTeam` (
    `TeamID` INT(5) NOT NULL,
    `Employee_idEmployee` INT(5) NOT NULL,
    `Project_ProjectName` VARCHAR(45) NOT NULL,
    PRIMARY KEY (`TeamID`, `Employee_idEmployee`, `Project_ProjectName`),
    CONSTRAINT `fk_ProjectTeam_Employee1`
    FOREIGN KEY (`Employee_idEmployee`)
    REFERENCES `EmployeeCompany`.`Employee` (`EM_ID`)
    ON DELETE CASCADE
    ON UPDATE NO ACTION,
    CONSTRAINT `fk_ProjectTeam_Project1`
    FOREIGN KEY (`Project_ProjectName`)
    REFERENCES `EmployeeCompany`.`Project` (`ProjectName`)
    ON DELETE CASCADE
    ON UPDATE NO ACTION
) ENGINE = InnoDB;

CREATE TABLE IF NOT EXISTS `EmployeeCompany`.`Salaried_Employee` (
    `Salary` INT(5) NOT NULL,
    `Employee_idEmployee` INT(5) NOT NULL,
    PRIMARY KEY (`Employee_idEmployee`),
    CONSTRAINT `fk_Salaried_Employee_Employee`
    FOREIGN KEY (`Employee_idEmployee`)
    REFERENCES `EmployeeCompany`.`Employee` (`EM_ID`)
    ON DELETE CASCADE
    ON UPDATE CASCADE
) ENGINE = InnoDB;

CREATE TABLE IF NOT EXISTS `EmployeeCompany`.`Hourly_Employee` (
    `Hourly_Pay` INT(5) NOT NULL,
    `Employee_idEmployee` INT(5) NOT NULL,
    PRIMARY KEY (`Employee_idEmployee`),
    CONSTRAINT `fk_Hourly_Employee_Employee`
    FOREIGN KEY (`Employee_idEmployee`)
    REFERENCES `EmployeeCompany`.`Employee` (`EM_ID`)
    ON DELETE CASCADE
    ON UPDATE CASCADE
) ENGINE = InnoDB;
```

## Usage

### Inserting Data

Here are some examples of how to insert data into the tables:

```sql
-- Inserting data into Manager table
INSERT INTO Manager (ManagerID, ManagerName) VALUES (1, 'John Doe');

-- Inserting data into Employee table
INSERT INTO Employee (EmployeeID, EmployeeName, Gender, DateOfBirth, PhoneNumber, Email, Age, Manager_ID)
VALUES (2, 'Jane', 'Smith', 'Female', '1995-05-20', 0505271638, 'jane.smith@example.com', 28, 1),

-- Inserting data into Department table
INSERT INTO Department (DepartmentID, DepartmentName) VALUES (HR, 'Human Resources');

-- Inserting data into JobRole table
INSERT INTO JobRole (JobName) VALUES ('HR Coordinator'),

-- Inserting data into Attendance table
INSERT INTO Attendance (AttendanceID, EmployeeID, Date, Time)
VALUES (1, 1, '2023-01-01', '09:00:00');

-- Inserting data into Project table
INSERT INTO Project (ProjectID, ProjectName, StartDate, EndDate)
VALUES  (1, '2023-01-15', '09:00:00', '17:00:00', 1),
```

### Basic Queries

You can query the database to retrieve information. Here are some example queries:

```sql
-- Select all employees
SELECT * FROM Employee;

-- Get all employees managed by a specific manager
SELECT * FROM Employee WHERE Manager_ID = 1;

```

## Conclusion

This project provides a solid foundation for managing an organization's employee data, allowing you to perform essential operations such as adding, updating, and querying information. It serves as a practical introduction to real-world database management system projects.

