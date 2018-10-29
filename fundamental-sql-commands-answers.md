#Exercises:

> 1. List the commands for adding, updating, and deleting data.

**Adding Data:**
```sql
INSERT INTO table (columns) VALUES (column-values)
```

**Updating Data:**
```sql
UPDATE table SET column-value(s) WHERE identifying-value(s)
```

**Deleting Data:**
```sql
DELETE FROM table WHERE identifying-value(s)
```

> 2. Explain the structure for each type of command.

**Adding Data:**
Inserts a list of rows containing values, separated by commas, corresponding to the column layout. 

**Updating Data:**
The SET command declares the value of the specified column in the row which matches the WHERE query.

**Deleting Data:**
This deletes the row which matches the WHILE query.

> 3. What are some of the data types that can be used in tables? Give a real-world example of each type.

**Text:**
Name of the contact in your address book
**Integer:**
Phone number of the contact
**Date:**
Birthday of the contact
**Timestamp:**
When the contact was last updated

> 4. Decide how to create a new table to hold a list of people invited to a wedding dinner. The table needs to have first and last names, whether they sent in their RSVP, the number of guests they are bringing, and the number of meals (1 for adults and 1/2 for children).

**Data Types:**

* First & Last name = text
* RSVP'ed = boolean
* \# guests = integer
* \# meals = integer

**Create table**

```sql
CREATE TABLE guestlist (
  firstname text,
  lastname text,
  guests integer,
  meals integer
);
```

**Add Thank you card column**

```sql
ALTER TABLE guestlist
ADD COLUMN thanked boolean
SET DEFAULT FALSE;
```

**Remove meals column**

```sql
ALTER TABLE guestlist
DROP COLUMN meals;
```

**Add table # column**

```sql
ALTER TABLE guestlist
ADD COLUMN tablenumber integer;
```

**Remove table # column**

```sql
ALTER TABLE guestlist
DROP COLUMN tablenumber;
```

> 5. Write a command to create a new table to hold the books in a library with the columns ISBN, title, author, genre, publishing date, number of copies, and available copies.

```sql
CREATE TABLE books (
  ISBN bigint,
  title text,
  author text,
  genre text,
  published date,
  copiestotal integer,
  copiesavail integer
);

-- Add 3 books

INSERT INTO books (ISBN, title, author, genre, published, copiestotal, copiesavail)
  VALUES
  (9780062255655, 'The Ocean at the End of the Lane', 'Neil Gaiman', 'Dark fantasy', DATE '2013-06-18', 1, 1),
  (9780066211312, 'Just Kids', 'Patti Smith', 'Memoir', DATE '2010-01-19', 1, 1),
  (0553103547 , 'A Game of Thrones', 'George R. R. Martin', 'Epic fantasy', DATE '1996-08-01', 1, 1);

-- Update quantity

UPDATE books
  SET copiesavail = copiesavail - 1
  WHERE ISBN = 9780066211312;

-- Ban a book

DELETE FROM books
  WHERE ISBN = 0553103547;
```

> 6. Write a command to make a new table to hold spacecrafts. Information should include id, name, year launched, country of origin, a brief description of the mission, orbiting body, if it is currently operating, and its approximate miles from Earth.

```sql
-- Create table

CREATE TABLE spacecrafts (
  id integer,
  name text,
  launched integer,
  origin text,
  mission text,
  orbiting text,
  is_operating boolean,
  proximity integer
);

-- Add 3 spacecrafts

INSERT INTO spacecrafts (id, name, launched, origin, mission, orbiting, operating, proximity)
  VALUES
  (1, '2001 Mars Odyssey', 2001, 'USA', 'Map the surface of Mars', 'Mars', TRUE, 33900000),
  (2, 'Pioneer 6', 1965, 'USA', 'Space weather monitor', 'Sun', FALSE, 92960000),
  (3, 'Venera 9', 1975, 'USSR', 'First spacecraft to orbit Venus. Atmospheric/Magnetic studies', 'Venus', TRUE, 162000000);

-- Remove one satellite

DELETE FROM spacecrafts
  WHERE id = 1;

-- Change operating status

UPDATE spacecrafts
  SET is_operating = !is_operating
  WHERE id = 3;
```

> 7. Write a command to create a new table to hold the emails in your inbox. This table should include an id, the subject line, the sender, any additional recipients, the body of the email, the timestamp, whether or not you have read the email, and the id of the email chain it's in.

```sql
-- Create table

CREATE TABLE inbox (
  id integer,
  subject text,
  sender text,
  recipients text[],
  body text,
  timestamp timestamp,
  is_read boolean,
  chainid integer
);

-- Add 3 emails

INSERT INTO inbox (id, subject, sender, recipients, body, timestamp, is_read, chainid)
  VALUES
  (11111, 'Test email 1', 'sender1@gmail.com', {}, 'This is a test email. Thanks!', TIMESTAMP '2018-10-28 10:33:13', FALSE, 12345),
  (22222, 'Test email 2', 'sender2@gmail.com', {'recipient1@hotmail.com', 'recipient2@yahoo.com'}, 'This is another test email. Cheers!', TIMESTAMP '2018-10-29 13:24:03', FALSE, 23456),
  (33333, 'Test email 3', 'sender3@gmail.com', {'recipient3@aol.com'}, 'This is YET ANOTHER test email. Sincerely, Matt.', TIMESTAMP '2018-10-29 07:22:45', FALSE, 34567);

-- Deleted an email

DELETE FROM inbox
  WHERE id = 22222;

-- Mark as read

UPDATE inbox
  SET is_read = TRUE
  WHERE id = 33333;

```