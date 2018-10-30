#Exercises

> 1. Write out a generic `SELECT` statement.

```sql
SELECT column(s)
  FROM tablename
  WHERE identifier operator value;
```

> 2. Create a fun way to remember the order of operations in a SELECT statement, such as a mnemonic.

SELECT-FROM-WHERE ... S-F-W ... Safe-For-Work 

> 3. Dog table

```sql
-- Display the name, gender, and age of all dogs that are part Labrador.

SELECT name, gender, age
  FROM dogs
  WHERE breed LIKE '%labrador%';

-- Display the ids of all dogs that are under 1 year old.

SELECT id
  FROM dogs
  WHERE age < 1;

-- Display the name and age of all dogs that are female and over 35lbs.

SELECT name, age
  FROM dogs
  WHERE gender = 'F' AND weight > 35;

-- Display all of the information about all dogs that are not Shepherd mixes.

SELECT *
  FROM dogs
  WHERE breed NOT LIKE '%shepherd%';

-- Display the id, age, weight, and breed of all dogs that are either over 60lbs or Great Danes.

SELECT id, age, weight, breed
  FROM dogs
  WHERE weight > 60 OR breed LIKE '%great dane%';
```

> 4. Cats table

`SELECT name, adoption_date FROM cats;`

| name     | adoption_date            |
| -------- | ------------------------ |
| Mushi    | 2016-03-22T00:00:00.000Z |
| Seashell | null                     |
| Azul     | 2016-04-17T00:00:00.000Z |
| Victoire | 2016-09-01T00:00:00.000Z |
| Nala     | null                     |

`SELECT name, age FROM cats;`

| name     | age |
| -------- | --- |
| Mushi    | 1   |
| Seashell | 7   |
| Azul     | 3   |
| Victoire | 7   |
| Nala     | 1   |

> 5. Cats table queries

```sql
-- Display all the information about all of the available cats.

SELECT *
  FROM cats
  WHERE adoption_date IS NULL;

-- Display the name and sex of all cats who are 7 years old.

SELECT name, gender
  FROM cats
  WHERE age = 7;

-- Find all of the names of the cats, so you don’t choose duplicate names for new cats.

SELECT name
  FROM cats;
```

> 6. List each comparison operator and explain when you would use it. Include a real world example for each.

Real world application: Voting survey

* **Equal to (=)**  
  Use when comparing exact values.
  Ex: Looking for all households where all have registered to vote (registered = TRUE)

* **Less Than (<)**  
  Use for comparing numbers or dates.
  Ex: Looking for households where the oldest member is younger than 50

* **Less Than or Equal to (<=)**
  Use for comparing numbers or dates.
  Ex: Looking for all households where the street number is less than or equal to 3200.

* **Greater Than(>)**
  Use for comparing numbers or dates.
  Ex: Looking for all households where the number of adults is greater than 2.

* **Greater Than or Equal to (>=)**
  Use for comparing numbers or dates.
  Ex: Looking for all households that have 1 or more children.

* **Not Equal to (!= , <>)**
  Use when comparing values that should not equal.
  Ex: Looking for all households that are registered to vote as anything but 'Democrat'

* **Partial Match (LIKE)**
  Use when comparing strings that may not be exact.
  Ex: Looking for all households with a last name starting with 'S'

> 7. From the cats table, what data is returned from these queries?

`SELECT name FROM cats WHERE gender = 'F';`

| name     |
| -------- |
| Seashell |
| Nala     |

`SELECT name FROM cats WHERE age <> 3;`

| name     |
| -------- |
| Mushi    |
| Seashell |
| Victoire |
| Nala     |

`SELECT ID FROM cats WHERE name != 'Mushi' AND gender = 'M';`

| id  |
| --- |
| 3   |
| 4   |