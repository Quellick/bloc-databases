#Exercises:

> 1. What data types do each of these values represent?

* "A Clockwork Orange" = string
* 42 = integer
* 09/02/1945 = date
* 98.7 = float
* $15.99 = float

> 2. Explain when a database would be used. Explain when a text file would be used.

A database would be used when data needs to persist after runtime. Also, if multiple systems or users are accessing the data at the same time, a database would be best. A text file is ideal in a situation where data only needs to be appended to the file and only one system needs to work with it.

> 3. Describe one difference between SQL and other programming languages.

SQL is a declarative programming language rather than a procedural language

> 4. In your own words, explain how the pieces of a database system fit together at a high level.

A database might contain several tables of data to be stored. The data can be accessed using queries to read or modify specific values in the table. The system then uses the most efficient method of returning or changing the data.

> 5. Explain the meaning of table, row, column, and value.

A table is a section of data in a database. The table has column headers which define or describe the data in them. Each row in the table contains values corresponding to the columns.


> 6. List three data types that can be used in a table.

Strings, ingegers, booleans

> 7. 

* Show all the dates and amounts for each payment

**Result:**

| date                     | amount    |
| ------------------------ | --------- |
| 2016-05-01T00:00:00.000Z | 1500.0000 |
| 2016-05-10T00:00:00.000Z | 37.0000   |
| 2016-05-15T00:00:00.000Z | 124.9300  |
| 2016-05-23T00:00:00.000Z | 54.7200   |

* Show only the payment amounts that are highter than $500 

**Result:**

| amount    |
| --------- |
| 1500.0000 |

* Show all payment data for the payee named 'Mega Foods'

**Result:**

| date                     | payee      | amount   | memo      |
| ------------------------ | ---------- | -------- | --------- |
| 2016-05-15T00:00:00.000Z | Mega Foods | 124.9300 | Groceries |

> 8. 

* The email and sign-up date for the user named DeAndre Data.

SELECT email, signup
FROM users
WHERE name = 'DeAndre Data';

**Result:**

| email             | signup                   |
| ----------------- | ------------------------ |
| datad@comcast.net | 2008-01-20T00:00:00.000Z |

* The user ID for the user with email 'aleesia.algorithm@uw.edu'.

SELECT userid
FROM users
WHERE email = 'aleesia.algorithm@uw.edu';

**Result:**

| userid |
| ------ |
| 1      |

* All the columns for the user ID equal to 4.

SELECT *
FROM users
WHERE userid = 4;

**Result:**

| userid | name           | email             | signup                   |
| ------ | -------------- | ----------------- | ------------------------ |
| 4      | Brandy Boolean | bboolean@nasa.gov | 1999-10-15T00:00:00.000Z |
