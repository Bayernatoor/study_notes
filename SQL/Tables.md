## creating a table:

Use: `CREATE TABLE` statement followed by the name of the table and the fields you want in the table.

EX:

`CREATE TABLE people(
  id INTEGER,
  tag TEXT,
  name TEXT,
  age INTEGER,
  balance INTEGER,
  is_admin BOOLEAN
);`

Note: Can also use INT but INTEGER is the standard-compliant keyword

=======================

- in a standard DB, it's typical to create 1 table per entity:
    - users, posts, comments, like

## Altering a table:

Use `ALTER TABLE` statement to make changes in place without deleting any data.

Rename table:

```
ALTER TABLE people
RENAME to users;
```


Rename column:

```
ALTER TABLE users
RENAME COLUMN tag TO username;
```


Add a column:

```
ALTER TABLE users
ADD COLUMN password TEXT;
```

=======================

## Migrations:

A migration is a change to the structure of the relational DB. It's similar to a commit in GIT but for the DB schema. 

ALTER TABLE is technically a MIGRATION.

- Migrations are especially important in team settings to ensure that everyone applies the same changes in the same order.
- A good migration should be small, incremental and ideally reversible

NOTE: A good migration needs to think about 2 things:
    1. The currently running version of the code.
    2. The new version of the code that runs after the migration.

Essentially make sure that your new migration doesn't break your old code. Prevent this by doing a MULTI-PHASED ROLLOUT.


1. Step 1 run migration to add new colum
2. Deploy new code that uses that new column but not the old column 
3. Step three cleanup the old column.

- It's not recommended to UPDATE an existing column. Like renaming a column actvely being used in prod. 

We should.

1. Run a migration with the new column name
2. Copy data from old column to new column
3. Deploy the code that uses the new column
4. recopy the data from old column to new column to capture anything that was missed during the inital copy and the code deploy.
5. step 5 run migration to clean the old column.

- Or, schedule downtime to update DB. This should be LAST result. Avoid downtime at all cost.


UP migrations: Moves the schema forward
DOWN migrations: Used to reverse the UP migration if it caused a problem. 
    - Rollbacks a change. 
    - A migration but in the the reverse order of te UP migration


If you write an UP migration you should write a DOWN migration to use in the case of a necessary rollback.

The DOWN migration will of course readd the removed column (if that was what the UP did) but it won't recover data. Need a backup for that!

==========================

## SQL DataTypes:

Different DBs support different Data Types.

SQLite Data Types:

NULL - Null value.
INTEGER - A signed integer stored in 0,1,2,3,4,6, or 8 bytes.
REAL - Floating point value stored as an 64-bit IEEE floating point number.
TEXT - Text string stored using database encoding such as UTF-8
BLOB - Short for Binary large object and typically used for images, audio or other multimedia.
BOOLEAN - Boolean values are written in SQLite queries as true or false, but are recorded as 1 or 0.






