# SQL VET EXERCISE

## Creating a table with vets, pets and visits

``` SQL
use ryan_db

-- VETS --> ID (PK), Email, phone no., name, location, speciality
-- PETS --> ID(PK), name, species, owner
-- VISITS --> ID(PK), Pet(FK), Vet(FK)

CREATE TABLE Vets
(
vet_ID INT NOT NULL IDENTITY(1,1) PRIMARY KEY,
first_name VARCHAR(20),
last_name VARCHAR(20),
email VARCHAR(100),
phone_No VARCHAR(15),
V_location VARCHAR(30),
speciality VARCHAR(30),
);

--ADD SOME VETS
INSERT INTO Vets
VALUES(
    'Jo', 'McDove', 'mcdove@gmail.com', '10290303', 'London', 'General'
),
(
    'Joana', 'Savana', 'joanavana@gmail.com', '10293942', 'Coventry', 'Surgery'
)
-- CHECK THEY EXIST
SELECT * FROM Vets

--PETS --> ID(PK), name, species, owner

CREATE TABLE Pets
(
pet_ID INT NOT NULL IDENTITY(1,1) PRIMARY KEY,
pet_name VARCHAR(40),
species VARCHAR(40),
pet_owner VARCHAR(40),
);

--ADD SOME PETS
INSERT INTO Pets
VALUES(
    'Ralph', 'Goat', 'Martha'
),
(
    'Ringo', 'Dogo', 'Phil'
)

-- CHECK THEY EXIST
SELECT * FROM Pets

-- VISITS --> ID(PK), Pet(FK), Vet(FK)
CREATE TABLE Visits(
visit_ID INT NOT NULL IDENTITY(1,1) PRIMARY KEY,
pet_ID int,
vet_ID int,
CONSTRAINT fk_pet_ID FOREIGN KEY (pet_ID) REFERENCES Pets(pet_ID),
CONSTRAINT fk_vet_ID FOREIGN KEY (vet_ID) REFERENCES Vets(vet_ID)
);

--ADD SOME VISITS
INSERT INTO Visits
VALUES(
    1, 1
),
(
    2,1
),
(
    2,2
)

-- CHECK IT WORKS
SELECT * FROM Visits

--ADD A NEW COLUMN Date
ALTER TABLE Visits
    ADD visit_day date;

-- UPDATE TABLE WITH NEW DATE COLUMN VALUES
UPDATE Visits
SET visit_day = '03-24-2019'
WHERE visit_id = 3
```
