# SQLProject
SQL Project and Querying

--Here some querying on creating table, stored procedures, and constraints

--Check back for updates

USE [AdventureWorks2012]
GO

CREATE Table tblPerson
( ID int NOT NULL Primary Key,
Name nvarchar (50) NOT NULL,
Email nvarchar (50) NOT NULL,
GenderID int
)

CREATE Table tblGender
(ID int NOT NULL Primary Key,
Gender nvarchar (50) NOT NULL)

ALTER TABLE tblGender
ADD CONSTRAINT fk_tbl_Gender Foreign Key (GenderID)
REFERENCES tblGender (ID)


INSERT INTO tblPerson (ID, Name, Email, GenderID) VALUES 
(1, 'Jade', 'j@j.com', 2)

INSERT INTO tblPerson (ID, Name, Email, GenderID) VALUES 
(2, 'Mary', 'm@m.com', 3)

INSERT INTO tblPerson (ID, Name, Email, GenderID) VALUES 
(3, 'Martin', 'ma@ma.com', 1)

INSERT INTO tblPerson (ID, Name, Email, GenderID) VALUES 
(4, 'Rob', 'r@r.com', NULL)

INSERT INTO tblPerson (ID, Name, Email, GenderID) VALUES 
(5, 'May', 'may@may.com', 2)

INSERT INTO tblPerson (ID, Name, Email, GenderID) VALUES 
(6, 'Kristy', 'k@k.com', 'NULL')

INSERT INTO tblGender (ID, Gender) VALUES
(1, 'Male')

INSERT INTO tblGender (ID, Gender) VALUES
(2, 'Female')

INSERT INTO tblGender (ID, Gender) VALUES
(3, 'Unknown')

-Default Constraint

--Using tables from video 3

SELECT * FROM tblPerson

SELECT * FROM tblGender


INSERT INTO tblPerson (ID, Name, Email, GenderID) VALUES
(7, 'Rich', 'r@r.com')

ALTER TABLE tblPerson ADD CONSTRAINT df_tblPerson_GenderID
DEFAULT 3 FOR GenderID


INSERT INTO tblPerson (ID, Name, Email, GenderID) VALUES
(8, 'Mike', 'mike@m.com')


--Check Constraint

--Using table tblperson 

SELECT * FROM tblPerson

INSERT INTO tblperson values (4, 'Sara', 's@s.com', 2, -170)

DELETE FROM tblPerson
WHERE ID =4

--Check Constraint

ALTER TABLE tblPerson
ADD CONSTRAINT ck_tbl_person_age CHECK (Age > 0 AND Age <150)

INSERT INTO tblperson values (4, 'Sara', 's@s.com', 2, 10)

--Check constraint allows NULL because I cannot compare NULL with anything

INSERT INTO tblperson values (4, 'Sara', 's@s.com', 2, NULL)


--Unique Key Constraint

--Use the tblPerson table

DROP TABLE tblPerson

CREATE Table tblPerson
( ID int NOT NULL Primary Key,
Name nvarchar (50) NOT NULL,
Email nvarchar (50) NOT NULL,
GenderID int,
Age int
)


INSERT INTO tblPerson (ID, Name, Email, GenderID, Age) VALUES 
(1, 'abc', 'j@j.com', 2, 20)

INSERT INTO tblPerson (ID, Name, Email, GenderID, Age) VALUES 
(2, 'wxyz', 'j@j.com', 1, 25)

--Unique Constraint

ALTER TABLE tblPerson
ADD CONSTRAINT uq_tblperson_email
UNIQUE (email)

--This will allow me to have one more email the same.  Now I have 2 emails that are j@j.com

INSERT INT tblPerson VALUES (2, 'wxyz', 'j@j.com', 20)


ALTER TABLE
DROP CONSTRAINT uq_tblperson_email


--Stored Procedures

CREATE TABLE tblEmployee
(Id int, 
Name nvarchar (25),
Gender nvarchar (20),
DepartmentId int)

INSERT INTO tblEmployee (Id, Name, Gender, DepartmentId) VALUES (1, 'Sam', 'Male', 1)

INSERT INTO tblEmployee (Id, Name, Gender, DepartmentId) VALUES (2, 'Ryan', 'Male', 1)

INSERT INTO tblEmployee (Id, Name, Gender, DepartmentId) VALUES (3, 'Sara', 'Female', 2)

INSERT INTO tblEmployee (Id, Name, Gender, DepartmentId) VALUES (4, 'Todd', 'Male', 2)

INSERT INTO tblEmployee (Id, Name, Gender, DepartmentId) VALUES (5, 'John', 'Male', 3)

INSERT INTO tblEmployee (Id, Name, Gender, DepartmentId) VALUES (6, 'Sana', 'Female', 2)

INSERT INTO tblEmployee (Id, Name, Gender, DepartmentId) VALUES (7, 'James', 'Male', 1)

INSERT INTO tblEmployee (Id, Name, Gender, DepartmentId) VALUES (8, 'Rob', 'Male', 2)

INSERT INTO tblEmployee (Id, Name, Gender, DepartmentId) VALUES (9, 'Steve', 'Male', 1)

INSERT INTO tblEmployee (Id, Name, Gender, DepartmentId) VALUES (10, 'Pam', 'Female', 2)

SELECT * FROM tblEmployee

CREATE Procedure spGetEmployee
AS
BEGIN
SELECT Name, Gender FROM tblEmployee
END

EXECUTE spGetEmployee

CREATE Procedure spGetEmployeeByGenderAndDepartment
@Gender nvarchar (20),
@DepartmentId int
AS

BEGIN
SELECT Name, Gender, DepartmentId FROM tblEmployee
WHERE Gender = @Gender AND DepartmentId = @DepartmentId

END

EXECUTE spGetEmployeeByGenderAndDepartment 'Male', 2

EXECUTE spGetEmployeeByGenderAndDepartment  @DepartmentId = 2, @Gender = 'Male'

Drop proc spGetEmployeeByGenderAndDepartment



CREATE Procedure spGetEmployeeByGenderAndDepartment
@Gender nvarchar (20),
@DepartmentId int
WITH ENCRYPTION
AS

BEGIN
SELECT Name, Gender, DepartmentId FROM tblEmployee
WHERE Gender = @Gender AND DepartmentId = @DepartmentId

END

--Stored Procedures with output parameters



CREATE PROCEDURE spGetEmployeeCountbyGender
@Gender nvarchar (20),
@EmployeeCount int OUTPUT
AS
BEGIN

SELECT EmployeeCount = COUNT(Id) 
FROM tblEmployee
WHERE Gender = @Gender

END

--To execute the stored procedure with output parameters

Declare @TotalCount int
EXECUTE spGetEmployeeCountbyGender 'Male', @TotalCount OUTPUT
PRINT @TotalCount


Declare @TotalCount int
EXECUTE spGetEmployeeCountbyGender 'Male', @TotalCount OUTPUT
if (@TotalCount is NULL)
PRINT '@TotalCount is NULL'
ELSE 
PRINT '@TotalCount is not NULL'

Declare @TotalCount int
EXECUTE spGetEmployeeCountbyGender 'Male', @TotalCount 
if (@TotalCount is NULL)
PRINT '@TotalCount is NULL'
ELSE 
PRINT '@TotalCount is not NULL'

DECLARE @TotalCount int
EXECUTE spGetEmployeeCountbyGender @EmployeeCount = @TotalCount out, @Gender = 'Male'
PRINT @TotalCount


--Stored Procedure output parameters or return values

--Use the same table

CREATE PROC spGetTotalCount1
@TotalCount int OUTPUT
AS
BEGIN
SELECT @TotalCount = COUNT(ID)
FROM tblEmployee
END

DECLARE @Total int
EXECUTE spGetTotalCount1 Out
Print @Total

CREATE PROCEDURE spGetTotalCount2
AS
BEGIN
RETURN (SELECT COUNT(ID) FROM tblEmployee)
END

DECLARE @Total int
EXECUTE @Total = spGetTotalCount2
PRINT @Total

--Write a stored procedure which gives the name of an employee when I give it an Id

CREATE PROCEDURE spGetNameById1
@Id int,
@Name nvarchar (20) output
AS
BEGIN

SELECT @Name = Name
FROM tblEmployee WHERE ID = @Id

END

DECLARE @Name nvarchar (20)
EXECUTE spGetNameById1 1, @Name Output
PRINT 'Name = ' + @Name

CREATE PROCEDURE spGetNameById2
@Id int
AS
BEGIN

RETURN (SELECT Name FROM tblEmployee WHERE Id = @Id)

END

DECLARE @Name nvarchar (20)
EXECUTE @Name = spGetNameById2
Print 'Name =' + @Name


SELECT * FROM tblEmployee



CREATE PROCEDURE spTotalCount1
@TotalCount int OUTPUT
AS
BEGIN
SELECT @TotalCount = COUNT(ID)
FROM tblEmployee
END

DECLARE @TotalEmployees int
EXECUTE spGetTotalCount1 @TotalEmployees OUT
PRINT @TotalEmployees
