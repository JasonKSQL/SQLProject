# SQLProject
SQL train and passenger schedule mini project

--Check back for updates

--I am working on the formatting.  

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




--TrainID       TrainName	SourceLocation	  DestinationLocation	   DepartureDate	DepartureTime

--1	            Train 1		Raleigh		        Toledo			           2018-09-24   	06:15:00.00

--2	            Train 2		Detroit		        Chicago		             2018-09-23	    06:15:00.00

--3	            Train 3		Raleigh		        Toledo			           2018-09-23	    06:15:00.00

--4	            Train 4		Atlanta		        Austin			           2018-09-28	    06:15:00.00

--5	            Train 5		Raleigh		        Orlando		             2018-09-30	    06:15:00.00


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



