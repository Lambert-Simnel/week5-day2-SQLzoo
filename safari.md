# Task - Safari Park

We've now seen how to set up and query a relational database, including how to set up links between our tables and query many tables at once. Now we'll put it into practice by building a database to store data in a specific format.

Usually we'll have a back-end application handling user input and communicating with the database. It will receive that input in a format known as **JSON** (**J**ava**S**cript **O**bject **N**otation) and determine how to structure a query based on that. In this task we will provide you with sample data which you should use as a guide to set up the tables. 

## The Data

Our users will be able to enter details for the animals in the park, their enclosures and the staff working there. Each member of staff will be assinged to a different enclosure on a different day; each enclosure will have more than one person looking after it. The data entered by the user will look like this:

```json
// animal

{
	"id": 1,
	"name": "Tony",
	"type": "Tiger",
	"age": 59,
	"enclosure_id": 1
}

// enclosure

{
	"id": 1,
	"name": "big cat field",
	"capacity": 20,
	"closedForMaintenance": false
}

// staff

{
	"id": 1,
	"name": "Captain Rik",
	"employeeNumber": 12345,
}

// assignment

{
	"id": 1,
	"employeeId": 1,
	"enclosureId": 1,
	"day": "Tuesday"
}
```

## MVP

- Draw an entity relationship diagram to show the structure of the tables and the relationships between them. Each table should have enough columns to capture all the data shown in the JSON above.
- Set up the tables in a postgres database. You can set them up using the `psql` REPL, a GUI like Postico or PGAdmin or by writing an SQL file like the one in the previous task.
CREATE TABLE staff (
	id SERIAL PRIMARY KEY,
	name VARCHAR(255),
	employee_number INT
);
CREATE TABLE enclosure (
	id SERIAL PRIMARY KEY,
	name VARCHAR(255),
	capacity INT,
	closedformaintenance BOOLEAN
);
CREATE TABLE animal (
	id SERIAL PRIMARY KEY,
	name VARCHAR(255),
	type VARCHAR(255),
	age INT,
	enclosureid INT REFERENCES enclosure(id)
);
CREATE TABLE assignment (
	id SERIAL PRIMARY KEY,
	employeeid INT REFERENCES staff(id),
	enclosureid INT REFERENCES enclosure(id),
	day VARCHAR(255)
);
- Populate the tables with some of your own data (you don't need to use more cereal mascots, unless you want to). Don't worry about the capacity restriction on enclosures for now, checking the would be handled by the back-end before the data gets sent to the database.
INSERT INTO staff (id, name, employee_number) VALUES (	1,	'Alfred',	2342	);
INSERT INTO staff (id, name, employee_number) VALUES (	2,	'Betty',	5647	);
INSERT INTO staff (id, name, employee_number) VALUES (	3,	'Carol',	4373	);
INSERT INTO staff (id, name, employee_number) VALUES (	4,	'Dexter',	6548	);
INSERT INTO staff (id, name, employee_number) VALUES (	5,	'Edward',	1436	);
INSERT INTO staff (id, name, employee_number) VALUES (	6,	'Francesca',	2375	);
INSERT INTO staff (id, name, employee_number) VALUES (	7,	'George',	5744	);
INSERT INTO staff (id, name, employee_number) VALUES (	8,	'Henry',	1344	);
INSERT INTO staff (id, name, employee_number) VALUES (	9,	'Isabella',	9028	);
INSERT INTO staff (id, name, employee_number) VALUES (	10,	'Jordan',	1234	);

INSERT INTO enclosure (name, capacity, closedformaintenance) VALUES ('Big Cat Field', 20, false);
INSERT INTO enclosure (name, capacity, closedformaintenance) VALUES ('Elephant Expanse', 30, false);
INSERT INTO enclosure (name, capacity, closedformaintenance) VALUES ('Zebra Plain', 15, true);
INSERT INTO enclosure (name, capacity, closedformaintenance) VALUES ('Monkey Mayhem', 50, false);
INSERT INTO enclosure (name, capacity, closedformaintenance) VALUES ('Giraffe Glade', 10, false);

INSERT INTO animal (id, name,type, age,enclosureid) VALUES (	1	,'	Anya Benjamin'	,'	Tiger'	,	5	,	1	);
INSERT INTO animal (id, name,type, age,enclosureid) VALUES (	2	,'	Hadley Pennington'	,'	Tiger'	,	3	,	1	);
INSERT INTO animal (id, name,type, age,enclosureid) VALUES (	3	,'	Brennen Beltran'	,'	Tiger'	,	12	,	1	);
INSERT INTO animal (id, name,type, age,enclosureid) VALUES (	4	,'	Kymani Mueller'	,'	Tiger'	,	23	,	1	);
INSERT INTO animal (id, name,type, age,enclosureid) VALUES (	5	,'	Brayden Osborne'	,'	Tiger'	,	7	,	1	);
INSERT INTO animal (id, name,type, age,enclosureid) VALUES (	6	,'	Brayan Little'	,'	Lion'	,	6	,	1	);
INSERT INTO animal (id, name,type, age,enclosureid) VALUES (	7	,'	Aedan Snyder'	,'	Lion'	,	5	,	1	);
INSERT INTO animal (id, name,type, age,enclosureid) VALUES (	8	,'	Lukas Lewis'	,'	Lion'	,	9	,	1	);
INSERT INTO animal (id, name,type, age,enclosureid) VALUES (	9	,'	Parker Klein'	,'	Indian Elephant'	,	11	,	2	);
INSERT INTO animal (id, name,type, age,enclosureid) VALUES (	10	,'	Rowan Cabrera'	,'	Indian Elephant'	,	13	,	2	);
INSERT INTO animal (id, name,type, age,enclosureid) VALUES (	11	,'	Luis Haley'	,'	Indian Elephant'	,	12	,	2	);
INSERT INTO animal (id, name,type, age,enclosureid) VALUES (	12	,'	Orion Gilmore'	,'	African Elephant'	,	5	,	2	);
INSERT INTO animal (id, name,type, age,enclosureid) VALUES (	13	,'	Rhianna Haynes'	,'	African Elephant'	,	3	,	2	);
INSERT INTO animal (id, name,type, age,enclosureid) VALUES (	14	,'	Terry House'	,'	African Elephant'	,	2	,	2	);
INSERT INTO animal (id, name,type, age,enclosureid) VALUES (	15	,'	Kiana Alvarez'	,'	African Elephant'	,	9	,	2	);
INSERT INTO animal (id, name,type, age,enclosureid) VALUES (	16	,'	Rylee Long'	,'	African Elephant'	,	5	,	2	);
INSERT INTO animal (id, name,type, age,enclosureid) VALUES (	17	,'	Nelson Whitney'	,'	African Elephant'	,	32	,	2	);
INSERT INTO animal (id, name,type, age,enclosureid) VALUES (	18	,'	Marin Vasquez'	,'	African Elephant'	,	54	,	2	);
INSERT INTO animal (id, name,type, age,enclosureid) VALUES (	19	,'	Fatima Turner'	,'	African Elephant'	,	2	,	2	);
INSERT INTO animal (id, name,type, age,enclosureid) VALUES (	20	,'	Bobby Duke'	,'	Zebra'	,	13	,	3	);
INSERT INTO animal (id, name,type, age,enclosureid) VALUES (	21	,'	Hana Craig'	,'	Zebra'	,	3	,	3	);
INSERT INTO animal (id, name,type, age,enclosureid) VALUES (	22	,'	Isaias Edwards'	,'	Zebra'	,	45	,	3	);
INSERT INTO animal (id, name,type, age,enclosureid) VALUES (	23	,'	Wayne Carney'	,'	Zebra'	,	6	,	3	);
INSERT INTO animal (id, name,type, age,enclosureid) VALUES (	24	,'	Albert Mathews'	,'	Zebra'	,	9	,	3	);
INSERT INTO animal (id, name,type, age,enclosureid) VALUES (	25	,'	Jazmyn Cisneros'	,'	Zebra'	,	21	,	3	);
INSERT INTO animal (id, name,type, age,enclosureid) VALUES (	26	,'	Osvaldo Gibbs'	,'	Zebra'	,	14	,	3	);
INSERT INTO animal (id, name,type, age,enclosureid) VALUES (	27	,'	Mia Riggs'	,'	Zebra'	,	2	,	3	);
INSERT INTO animal (id, name,type, age,enclosureid) VALUES (	28	,'	Clarissa Yoder'	,'	Gorilla'	,	41	,	4	);
INSERT INTO animal (id, name,type, age,enclosureid) VALUES (	29	,'	Juan Galvan'	,'	Gorilla'	,	5	,	4	);
INSERT INTO animal (id, name,type, age,enclosureid) VALUES (	30	,'	Noel Vaughn'	,'	Gorilla'	,	7	,	4	);
INSERT INTO animal (id, name,type, age,enclosureid) VALUES (	31	,'	Byron Gregory'	,'	Gorilla'	,	3	,	4	);
INSERT INTO animal (id, name,type, age,enclosureid) VALUES (	32	,'	Koen Shea'	,'	Manque'	,	7	,	4	);
INSERT INTO animal (id, name,type, age,enclosureid) VALUES (	33	,'	Pierre Shaw'	,'	Manque'	,	9	,	4	);
INSERT INTO animal (id, name,type, age,enclosureid) VALUES (	34	,'	Jazlynn Fox'	,'	Manque'	,	2	,	4	);
INSERT INTO animal (id, name,type, age,enclosureid) VALUES (	35	,'	Ashlynn Velazquez'	,'	Manque'	,	4	,	4	);
INSERT INTO animal (id, name,type, age,enclosureid) VALUES (	36	,'	Andreas Mercer'	,'	Manque'	,	34	,	4	);
INSERT INTO animal (id, name,type, age,enclosureid) VALUES (	37	,'	Cole Schmidt'	,'	Manque'	,	12	,	4	);
INSERT INTO animal (id, name,type, age,enclosureid) VALUES (	38	,'	Amber Mckee'	,'	Giraffes'	,	16	,	5	);
INSERT INTO animal (id, name,type, age,enclosureid) VALUES (	39	,'	Anaya Hamilton'	,'	Giraffes'	,	19	,	5	);
INSERT INTO animal (id, name,type, age,enclosureid) VALUES (	40	,'	Miles Bernard'	,'	Giraffes'	,	21	,	5	);

INSERT INTO assignment (employeeid, enclosureid, day) VALUES (1, 3, 'Monday');
INSERT INTO assignment (employeeid, enclosureid, day) VALUES (1, 2, 'Tuesday');
INSERT INTO assignment (employeeid, enclosureid, day) VALUES (1, 3, 'Wednesday');
INSERT INTO assignment (employeeid, enclosureid, day) VALUES (2, 1, 'Monday');
INSERT INTO assignment (employeeid, enclosureid, day) VALUES (2, 3, 'Thursday');
INSERT INTO assignment (employeeid, enclosureid, day) VALUES (2, 2, 'Friday');
INSERT INTO assignment (employeeid, enclosureid, day) VALUES (3, 5, 'Wednesday');
INSERT INTO assignment (employeeid, enclosureid, day) VALUES (4, 3, 'Tuesday');
INSERT INTO assignment (employeeid, enclosureid, day) VALUES (4, 4, 'Wednesday');
INSERT INTO assignment (employeeid, enclosureid, day) VALUES (4, 1, 'Thursday');
INSERT INTO assignment (employeeid, enclosureid, day) VALUES (4, 1, 'Friday');
INSERT INTO assignment (employeeid, enclosureid, day) VALUES (5, 2, 'Thursday');
INSERT INTO assignment (employeeid, enclosureid, day) VALUES (5, 2, 'Friday');
INSERT INTO assignment (employeeid, enclosureid, day) VALUES (6, 4, 'Tuesday');
INSERT INTO assignment (employeeid, enclosureid, day) VALUES (6, 2, 'Saturday');
INSERT INTO assignment (employeeid, enclosureid, day) VALUES (6, 3, 'Sunday');
INSERT INTO assignment (employeeid, enclosureid, day) VALUES (7, 5, 'Friday');
INSERT INTO assignment (employeeid, enclosureid, day) VALUES (7, 5, 'Saturday');
INSERT INTO assignment (employeeid, enclosureid, day) VALUES (7, 5, 'Sunday');
INSERT INTO assignment (employeeid, enclosureid, day) VALUES (8, 2, 'Thursay');
INSERT INTO assignment (employeeid, enclosureid, day) VALUES (8, 4, 'Sunday');
INSERT INTO assignment (employeeid, enclosureid, day) VALUES (9, 3, 'Wednesday');
INSERT INTO assignment (employeeid, enclosureid, day) VALUES (9, 1, 'Thursday');
INSERT INTO assignment (employeeid, enclosureid, day) VALUES (9, 2, 'Saturday');
INSERT INTO assignment (employeeid, enclosureid, day) VALUES (10, 5, 'Tuesday');
INSERT INTO assignment (employeeid, enclosureid, day) VALUES (10, 2, 'Monday');
INSERT INTO assignment (employeeid, enclosureid, day) VALUES (10, 4, 'Wednesday');
- Write queries to find:
	- The names of the animals in a given enclosure
	SELECT name FROM animal WHERE enclosureid = 3;
	- The names of the staff working in a given enclosure
	SELECT DISTINCT staff.name FROM staff LEFT JOIN assignment ON staff.id = assignment.employeeid WHERE assignment.enclosureid = 2;

	
## Extensions

Write queries to find:

- The names of staff working in enclosures which are closed for maintenance
SELECT DISTINCT staff.name FROM staff LEFT JOIN assignment ON staff.id = assignment.employeeid INNER JOIN enclosure ON assignment.enclosureid = enclosure.id WHERE enclosure.closedformaintenance = true;
- The name of the enclosure where the oldest animal lives. If there are two animals who are the same age choose the first one alphabetically.
SELECT enclosure.name FROM enclosure LEFT JOIN animal ON animal.enclosureid = enclosure.id ORDER BY animal.age DESC LIMIT 1;
- The number of different animal types a given keeper has been assigned to work with.
SELECT COUNT(DISTINCT animal.type) FROM animal INNER JOIN assignment ON animal.enclosureid = assignment.enclosureid WHERE assignment.employeeid = 4;
- The number of different keepers who have been assigned to work in a given enclosure
SELECT COUNT(DISTINCT employeeid) FROM assignment WHERE enclosureid = 2;
- The names of the other animals sharing an enclosure with a given animal (eg. find the names of all the animals sharing the big cat field with Tony)
SELECT name FROM animal WHERE enclosureid = (SELECT enclosureid FROM animal WHERE name LIKE '%Bobby Duke%') AND NOT id = (SELECT id FROM animal WHERE name LIKE '%Bobby Duke%');

## Hints

- Don't be tempted to perform too many joins, think about the data stored in each table.
- Remember that the result of a join is just another table. It can be filtered, ordered, summarised and joined again as much as you need.