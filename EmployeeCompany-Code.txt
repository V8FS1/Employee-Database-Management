SET @OLD_UNIQUE_CHECKS=@@UNIQUE_CHECKS, UNIQUE_CHECKS=0;
SET @OLD_FOREIGN_KEY_CHECKS=@@FOREIGN_KEY_CHECKS, FOREIGN_KEY_CHECKS=0;
SET @OLD_SQL_MODE=@@SQL_MODE, SQL_MODE='ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION';

CREATE SCHEMA IF NOT EXISTS `EmployeeCompany` DEFAULT CHARACTER SET utf8;
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

INSERT INTO `EmployeeCompany`.`Maneger` (`ManagerID`, `ManegeName`) VALUES
 (1, 'John Doe'),
 (5, 'Charli Brown');

 INSERT INTO `EmployeeCompany`.`Employee` (`EM_ID`, `FirstName`, `LastName`, `Gender`, `DateOfBirth`, `Phone`, `Email`, `Age`, `Maneger_ID`) VALUES
  (1, 'John', 'Doe', 'Male', '1990-01-15', 1234567890, 'john.doe@example.com', 32, Null),
  (2, 'Jane', 'Smith', 'Female', '1995-05-20', 0505271638, 'jane.smith@example.com', 28, 1),
  (3, 'Bob', 'Johnson', 'Male', '1985-09-10', 0508271938, 'bob.johnson@example.com', 38, 5),
  (4, 'Alice', 'Williams', 'Female', '1992-12-05', 0539127933, 'alice.williams@example.com', 31, 5),
  (5, 'Charlie', 'Brown', 'Male', '1988-07-25', 0599274393, 'charlie.brown@example.com', 35, NULL);

 INSERT INTO `EmployeeCompany`.`Department` (`DepartmentID`, `DepartmentName`) VALUES
 ('IT', 'Information Technology'),
 ('HR', 'Human Resources'),
 ('FM', 'Finance management');


 INSERT INTO `EmployeeCompany`.`JobRole` (`JobName`) VALUES
('IT Specialist'),
('HR Coordinator'),
 ('Accountant');


 INSERT INTO `EmployeeCompany`.`Salaried_Employee` (`Salary`, `Employee_idEmployee`) VALUES
 (120000, 1),
 (55000, 2),
 (70000, 4);


 INSERT INTO `EmployeeCompany`.`Hourly_Employee` (`Hourly_Pay`, `Employee_idEmployee`) VALUES
 (20, 3),
 (18, 5);

 INSERT INTO `EmployeeCompany`.`Project` (`ProjectName`, `ProjectStartDate`, `ProjectEndDate`) VALUES
 ('Project A', '2023-02-01', '2023-04-30'),
 ('Project B', '2023-03-15', '2023-06-30'),
 ('Project C', '2023-04-10', '2023-07-15');


 INSERT INTO `EmployeeCompany`.`JobRole_Department` (`JobRoleDepartmentID`, `JobRole_JobName`, `Department_ID`, `Employee_idEmployee`, `StartDate`, `EndDate`) VALUES
 (1, 'IT Specialist', 'IT', 1, '2016-11-16', '2020-04-12'),
 (2, 'HR Coordinator', 'HR', 2, '2017-06-09', '2019-07-19'),
 (3, 'Accountant', 'FM', 4, '2019-04-12', '2021-10-01'),
(4, 'HR Coordinator', 'HR', 3,'2018-05-20', '2020-08-03'),
 (5,'Accountant', 'FM', 5, ' 2015-07-12', '2022-04-28');

 INSERT INTO `EmployeeCompany`.`Attandance` (`AID`, `Date`, `ClockInTime`, `ClockOutTime`, `Employee_idEmployee`) VALUES
 (1, '2023-01-15', '09:00:00', '17:00:00', 1),
 (2, '2023-01-15', '09:30:00', '18:00:00', 2),
 (3, '2023-01-15', '10:00:00', '16:30:00', 3),
(4, '2023-01-15', '08:45:00', '17:15:00', 4),
 (5, '2023-01-15', '09:15:00', '17:45:00', 5);

 INSERT INTO `EmployeeCompany`.`ProjectTeam` (`TeamID`, `Employee_idEmployee`, `Project_ProjectName`) VALUES
 (1, 1, 'Project A'),
 (1, 2, 'Project A'),
 (2, 3, 'Project B'),
 (2, 4, 'Project B'),
 (2, 5, 'Project C');


SET SQL_MODE=@OLD_SQL_MODE;
SET FOREIGN_KEY_CHECKS=@OLD_FOREIGN_KEY_CHECKS;
SET UNIQUE_CHECKS=@OLD_UNIQUE_CHECKS;
