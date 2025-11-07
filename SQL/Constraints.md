# Constraints:

A constraint is a rule we create on our DB that enforces some speficic behaviour. 

Ex: Setting a NOT NULL constraint on a column, ensures that the column cannot accept NULL values.

## Defining a constraint on SQLite DB:

```
CREATE TABLE employees(
    id INTEGER PRIMARY KEY,
    -- The PRIMARY KEY constraint uniquely identifies each row in the table
    name TEXT UNIQUE,
    -- The UNIQUE constraint ensures that no two rows can have the same value in the 'name' column
    title TEXT NOT NULL
    -- The NOT NULL constraint ensures that the 'title' column cannot have NULL values
);
```

Not SQLite does no allow one to add a constraint via `ALTER TABLE` command. Must be added at table creation.

List of SQL commands no permitted by SQLite: https://www.sqlite.org/omitted.html

## Primary Keys:

A key defines and protects relationships between tables.

Primary Key: special column that uniquely identifies records within a table. *1 per table max*.

Primary key is almost always `id`. This means no 2 rows in that table can share the same `id`.

Role: 

- establish the main identity of each record (row)
- improves indexing and query performance
- typically the target of foreign keys in other tables. 


## Foreign Keys:

Foreign keys make relational DBs relational :) 

A FG in 1 table references a PK in another table.

EX in SQLite:

```
CREATE TABLE departments (
    id INTEGER PRIMARY KEY,
    department_name TEXT NOT NULL
);

CREATE TABLE employees (
    id INTEGER PRIMARY KEY,
    name TEXT NOT NULL,
    department_id INTEGER,
    CONSTRAINT fk_departments
    FOREIGN KEY (department_id)
    REFERENCES departments(id)
);
```
docs: https://www.sqlite.org/lang_createtable.html#constraint_enforcement


## Schema:

Describes how data within the DB is organized: https://www.ibm.com/think/topics/database-schema

There's no perfect way to architect a schema, no "correct" solution. But you try to choose sane table names, fields, constraints which best suite our project goal. 

Different schema designs comes with different trade-offs


## Relational DBs:

A DB that stores data so that it can easily be related to other other. 

Ex: A user can have many tweets. A relationship exists between users and tweets.

### Relational vs non-relational:

The big difference between relational and non-relational databases is that non-relational databases nest their data.

Oversimplication: non-relational DBs are like giant JSON blobs.

Ex: 

```
{
  "users": [
    {
      "id": 0,
      "name": "Elon",
      "courses": [
        {
          "name": "Biology",
          "id": 0
        },
        {
          "name": "Biology",
          "id": 0
        }
      ]
    }
  ]
}
```
