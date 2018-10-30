#Exercises:

> 1. How do you find related data held in two separate data tables?

Use the `JOIN` statement to match rows to column values

> 2. Explain, in your own words, the difference between an `INNER JOIN`, `LEFT OUTER JOIN`, and `RIGHT OUTER JOIN`. Give a real-world example for each.

Real world scenario: Movie theater database with 'movies' and 'screens' tables

`INNER JOIN`:
Outputs a row for each common matching row it finds. Ignores others. This is the default method.
Ex: Selecting all movies that are currently asssigned to a screen room

`LEFT OUTER JOIN`:
Outputs a row for every row in the first table, regardless of whether there is a matching row in the second table. `null` values are entered as the value for any which do not have a matching value in the second table.
Ex: Selecting movies that have not yet been assigned a screen room

`RIGHT OUTER JOIN`:
This functions the same as `LEFT OUTER JOIN` except the opposite. Rows are created for every row in the second table.
Ex: Listing all screen rooms even if there are no movies assigned to them

> 3. Define primary key and foreign key. Give a real-world example for each.
Define aliasing.

A **Primary key** is the column choice which ties the joined tables together with a unique identifier for each row.

A **foreign key** is the column chosen on the first table which connects to the primary key(s) on the other tables.

> 4. Define aliasing.

**Aliasing** is used to shorten table names in order to clean up the statements, stated with the `AS` keyword.

> 5. Change this query so that you are using aliasing:

```sql
SELECT p.name, c.salary, c.vacation_days
  FROM professor AS p
  JOIN compensation AS c
  ON p.id = c.professor_id;
```
> 6. Why would you use a `NATURAL JOIN`? Give a real-world example.

`NATURAL JOIN` is used as a shorthand for `USING` when you want to return only the columns which match in both input tables once.
Ex: Database for a group of franchised mechanic shops with tables for work_orders (order_number, description, cost, customer_id, phone_number), and customers (customer_id, location, name, phone_number). Naturally joining this would display the customer_id and phone_number columns only once, along with the others.

> 7. Employee schema

```sql
SELECT s.date, s.start_time, s.end_time, e.name
  FROM shifts as s
  JOIN scheduled_shifts AS ss
  ON s.id = ss.shift_id
  JOIN employees AS e
  ON e.id = ss.employee_id;
```
> 8. Adoptions schema

```sql
-- Create a list of all volunteers. If the volunteer is fostering a dog, include each dog as well.

SELECT v.first_name, v.last_name, d.name
  FROM volunteers as v
  LEFT OUTER JOIN dogs as d
  ON d.id = v.foster_dog_id;
```
**Results**

| first_name | last_name  | name      |
| ---------- | ---------- | --------- |
| Rubeus     | Hagrid     | Munchkin  |
| Marjorie   | Dursley    | Marmaduke |
| Sirius     | Black      |           |
| Remus      | Lupin      |           |
| Albus      | Dumbledore |           |

```sql
-- The cat's name, adopter's name, and adopted date for each cat adopted within the past month to be displayed as part of the "Happy Tail" social media promotion which posts recent successful adoptions.

SELECT c.name, a.first_name, a.last_name, ca.date
  FROM cat_adoptions AS ca
  JOIN cats AS c
  ON c.id = ca.cat_id
  JOIN adopters AS a
  ON a.id = ca.adopter_id;
```
**Results**

| name     | first_name | last_name | date                     |
| -------- | ---------- | --------- | ------------------------ |
| Azul     | Hermione   | Granger   | 2018-09-15T00:00:00.000Z |
| Mushi    | Arabella   | Figg      | 2018-10-10T00:00:00.000Z |
| Victoire | Argus      | Filch     | 2018-10-15T00:00:00.000Z |

```sql
-- Create a list of adopters who have not yet chosen a dog to adopt.

SELECT a.first_name, a.last_name
  FROM adopters AS a
  LEFT OUTER JOIN dog_adoptions as da
  ON da.adopter_id = a.id
  WHERE da.adopter_id IS NULL;
```
**Results**

| first_name | last_name |
| ---------- | --------- |
| Hermione   | Granger   |
| Arabella   | Figg      |

```sql
-- Lists of all cats and all dogs who have not been adopted.

SELECT c.name
  FROM cats AS c
  LEFT OUTER JOIN cat_adoptions AS ca
  ON ca.cat_id = c.id
  WHERE ca.adopter_id IS NULL;  

SELECT d.name
  FROM dogs AS d
  LEFT OUTER JOIN dog_adoptions AS da
  ON da.dog_id = d.id
  WHERE da.adopter_id IS NULL;
```
**Results (cats)**

| name     |
| -------- |
| Seashell |
| Nala     |

**Results (dogs)**

| name      |
| --------- |
| Munchkin  |
| Boujee    |
| Lassie    |
| Marley    |
| Marmaduke |

```sql
-- The name of the person who adopted Rosco.

SELECT a.first_name, a.last_name
  FROM adopters AS a
  JOIN dog_adoptions AS da
  ON da.adopter_id = a.id
  JOIN dogs AS d
  ON d.id = da.dog_id
  WHERE d.name = 'Rosco';
```
**Results**

| first_name | last_name |
| ---------- | --------- |
| Argus      | Filch     |

> 9. Library schema

```sql
-- To determine if the library should buy more copies of a given book, please provide the names and position, in order, of all of the patrons with a hold (request for a book with all copies checked out) on "Advanced Potion-Making".

SELECT p.name, h.rank
  FROM holds AS h
  JOIN patrons AS p
  ON p.id = h.patron_id
  JOIN books AS b
  ON b.isbn = h.isbn
  WHERE b.title = 'Advanced Potion-Making'
  ORDER BY h.rank ASC;
```
**Results**

| name           | rank |
| -------------- | ---- |
| Terry Boot     | 1    |
| Cedric Diggory | 2    |

```sql
-- List all of the library patrons. If they have one or more books checked out, list the books with the patrons.

SELECT DISTINCT p.name, CASE WHEN t.checked_in_date IS NULL
  	THEN b.title ELSE NULL
    END AS checked_out_title
  FROM patrons AS p
  JOIN transactions AS t
  ON t.patron_id = p.id
  JOIN books AS b
  ON b.isbn = t.isbn
  ORDER BY p.name ASC;
```
**Results**

| name             | checked_out_title                       |
| ---------------- | --------------------------------------- |
| Cedric Diggory   | Fantastic Beasts and Where to Find Them |
| Cho Chang        |                                         |
| Hermione Granger |                                         |
| Padma Patil      |                                         |
| Terry Boot       | Advanced Potion-Making                  |