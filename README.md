## Question 1
---
![](Images/one.JPG)
### CODE :
```
CREATE TABLE BUSINESS (
    business_name varchar(255),
    store_id varchar(255),
    PRIMARY KEY (store_id)
);

CREATE TABLE STORES (
    store_id varchar(255),
    total_deliveries int,
    PRIMARY KEY (store_id)
);



INSERT INTO BUSINESS
VALUES 
("business_1", "store_1"),
("business_1", "store_2"),
("business_1", "store_3"),
("business_2", "store_4"),
("business_3", "store_5"),
("business_3", "store_6");


INSERT INTO STORES
VALUES 
("store_1", 500),
( "store_2", 3000),
("store_3", 25),
( "store_4", 62),
("store_5", 8300),
("store_6", 650);



SELECT B.business_name, SUM(S.total_deliveries) as sum_deliveries
FROM BUSINESS B
INNER JOIN STORES S
ON B.store_id = S.store_id
GROUP BY B.business_name
ORDER BY sum_deliveries desc
LIMIT 5;

```
## Question 2
---
![](Images/two.JPG)

```

CREATE TABLE Constellations (
    Constellation varchar(255),
    Star varchar(255),
    PRIMARY KEY (Star)
);

CREATE TABLE Stars (
    Star varchar(255),
    Apparent_Magnitude float,
    PRIMARY KEY (Star)
);



INSERT INTO Constellations
VALUES 
("Scorpius", "Antares A"),
("Scorpius", "bow B"),
("Draco", "cow C"),
("Draco", "Dog D"),
("Draco", "Eli E"),
("Hydra", "fang");


INSERT INTO Stars
VALUES 
("Antares A", 0.91),
( "bow B", 1.62),
("cow C", 2.24),
( "Dog D", 2.73),
("Eli E", 2.79),
("fang", 1.99);



SELECT C.Constellation, AVG(S.Apparent_Magnitude) as avg_apparent_magnitude
FROM Constellations C
INNER JOIN Stars S
ON C.Star = S.Star
GROUP BY C.Constellation
HAVING avg_apparent_magnitude >= 0 AND avg_apparent_magnitude <= 10;
```

## Question 3

![](Images/three.JPG)

```

CREATE TABLE Audit_Log (
    Employee_ID int,
    Date date,
    Event_Type_ID int
);

CREATE TABLE Event_Types (
    Event_Type_ID int,
    Event_Type varchar(255)
);



INSERT INTO Audit_Log
VALUES 
(111, 01-01-2020, 5),
(112, 03-15-2020, 8),
(111, 02-19-2020, 5),
(114, 01-23-2020, 150),
(115, 02-15-2020, 100),
(111, 01-10-2020, 5);


INSERT INTO Event_Types
VALUES 
(1, "Create"),
(2, "Update"),
(3, "Delete"),
(4, "View"),
(5, "Share"),
(6, "Activate");



SELECT Employee_ID
FROM Audit_Log
GROUP BY Employee_ID
Having Event_Type_ID = 
(
SELECT Event_Type_ID
FROM Event_Types
WHERE Event_Type = "Share"
)
AND COUNT(Event_Type_ID) >= 1;
```
