# SQLProject
SQL Project and Querying


--Check back for updates

SQL Train and Passenger Project

Create Database TrainPassenger

CREATE TABLE Train
(TrainID int Primary Key,
TrainName varchar (50),
SourceLocation varchar (50),
DestinationLocation varchar (50),
DepartureDate date,
DepartureTime time)

SELECT * FROM Train


INSERT INTO Train VALUES ( 1, 'Train 1', 'Raleigh', 'Toledo', '09-24-2018', '6:15:00 PM')
INSERT INTO Train VALUES ( 2, 'Train 2', 'Detroit', 'Chicago','09-23-2018', '3:15:00 PM')
INSERT INTO Train VALUES ( 3, 'Train 3', 'Raleigh', 'Toledo', '09-23-2018', '4:15:00 PM')
INSERT INTO Train VALUES ( 4, 'Train 4', 'Atlanta', 'Austin', '09-28-2018', '2:15:00 PM')
INSERT INTO Train VALUES ( 5, 'Train 5', 'Raleigh', 'Orlando', '09-30-2018', '1:15:00 PM')


--This is the result I get
--TrainID  TrainName	SourceLocation	  DestinationLocation	   DepartureDate	DepartureTime
--1	       Train 1		Raleigh		        Toledo			           2018-09-24   	06:15:00.00
--2	       Train 2		Detroit		        Chicago		             2018-09-23	    06:15:00.00
--3	       Train 3		Raleigh		        Toledo			           2018-09-23	    06:15:00.00
--4	       Train 4		Atlanta		        Austin			           2018-09-28	    06:15:00.00
--5	       Train 5		Raleigh		        Orlando		             2018-09-30	    06:15:00.00


CREATE TABLE Passenger
(TrainID int,
PassengerID varchar (50) Primary Key,
PName varchar (50),
SeatNumber varchar (50),
TicketNumber varchar (20),
Fare INT
)





ALTER TABLE Passenger
ADD CONSTRAINT FK_Passenger_TrainID FOREIGN KEY (TrainID) REFERENCES Train (TrainID) 

SELECT * FROM Passenger

INSERT INTO Passenger VALUES ( 1, 'p1', 'John', 'A1', 'T1', 400)
INSERT INTO Passenger VALUES ( 2, 'p2', 'Mary', 'A2', 'T2', 560)
INSERT INTO Passenger VALUES ( 3, 'p3', 'Sara', 'A3', 'T3', 600)
INSERT INTO Passenger VALUES ( 2, 'p4', 'Mike', 'A4', 'T4', 300)
INSERT INTO Passenger VALUES ( 1, 'p5', 'David', 'A5', 'T5', 1200)
INSERT INTO Passenger VALUES ( 4, 'p6', 'Susan', 'A6', 'T6', 500)
INSERT INTO Passenger VALUES ( 5, 'p7', 'Steve', 'A7', 'T7', 300)
INSERT INTO Passenger VALUES ( 2, 'p8', 'Kelly', 'A8', 'T8', 200)
INSERT INTO Passenger VALUES ( 3, 'p9', 'Debbie', 'A9', 'T9', 700)
INSERT INTO Passenger VALUES ( 2, 'p10', 'Michelle', 'A10', 'T10', 800)
INSERT INTO Passenger VALUES ( 4, 'p11', 'Larry', 'A11', 'T11', 900)
INSERT INTO Passenger VALUES ( 5, 'p12', 'Bill', 'A12', 'T12', 560)
INSERT INTO Passenger VALUES ( 1, 'p13', 'Megan', 'A13', 'T13', 600)

--This is the result I get
--TrainID 	PassengerID 	PName 		SeatNumber 	 TicketNumber 		Fare
--	1	      p1		        John		  A1		        T1			        400
--	2	      p10		        Michelle	A10		        T10			        800
--	4	      p11		        Larry		  A11		        T11			        900
--	5	      p12		        Bill		  A12		        T12			        560
--	1	      p13		        Megan		  A13		        T13			        600
--	2	      p2		        Mary		  A2		        T2			        560
--	3	      p3		        Sara		  A3		        T3			        600
--	2	      p4		        Mike		  A4		        T4			        300
--	1	      p5		        David		  A5		        T5			        1200
--	4	      p6		        Susan		  A6		        T6			        500
--	5	      p7		        Steve		  A7		        T7			        300
--	2	      p8		        Kelly		  A8		        T8			        200
--	3	      p9		        Debbie		A9			      T9			        700



--If I wanted find out what the train names that are departing between '3:00 PM' and '6:15 PM
--and 09-23-2018 and 09-26-2018 it will look like this


SELECT TrainName
FROM Train
WHERE DepartureTime between '3:00:00 PM' and '6:15:00 PM'
And DepartureDate between '09-23-2018' and '09-26-2018'

--The results would like this

--  TrainName
--	Train 1
--	Train 2
--	Train 3

--If I want to find out train ID has a fare that ranges from 400 to 1000.  This is what it
--would look like


SELECT TrainID, Fare
FROM Passenger
WHERE Fare >400 and Fare <1000
ORDER BY Fare asc

--The results would like this

-- TrainID 	Fare
--	4	      500
--	2	      560
--	5	      560
--	1	      600
--	3	      600
--	3	      700
--	2	      800
--	4	      900



--If I wanted to match the ticket number with train ID it would like this


SELECT Train.TrainID, Passenger.TicketNumber
FROM Train, Passenger
WHERE Train.TrainID = Passenger.TrainID
ORDER BY TrainID

--The results would like this

--TrainID 	TicketNumber
--	1	      T1
--	1	      T13
--	1	      T5
--	2	      T2
--	2	      T10
--	2	      T8
--	2	      T4
--	3	      T9
--	3	      T3
--	4	      T6
--	4	      T11
--	5	      T12
--	5	      T7


--If I wanted to get the TrainID and TrainName from the Train Table 
--find out what the fare would be this is what it would look like


SELECT Train.TrainID, Train.TrainName, Passenger.Fare
FROM Train, Passenger
WHERE Train.TrainID = Passenger.TrainID


--The results would look like this

--TrainID 	TrainName 	Fare
--	1	        Train 1		400
--	2	        Train 2		800
--	4	        Train 4		900
--	5	        Train 5		560
--	1	        Train 1		600
--	2	        Train 2		560
--	3	        Train 3		600
--	2	        Train 2		300
--	1	        Train 1		1200
--	4	        Train 4		500
--	5	        Train 5		300
--	2	        Train 2		200
--	3	        Train 3		700

--If I want to find out how much money each train ID made this is what it looks like

SELECT TrainID, SUM(Fare) AS 'Fare Earned by Each Train'
FROM Passenger
GROUP BY TrainID
ORDER BY SUM (Fare) ASC

--The results would look like this

--TrainID 	Fare Earned by Each Train
--	5	       860
--	3	      1300
--	4	      1400
--	2	      1860
--	1	      2200

--End of SQL Project



--The following is querying SQL

--Here some querying on creating table, stored procedures, and constraints

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
