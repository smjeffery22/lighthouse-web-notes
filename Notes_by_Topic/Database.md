# DATABASE (LHL W4-W5)

## **DAY WE COMPASS NOTES**

### RELATIONAL DATABASE
* Data is stored in database in an organized way in tables
  * **Search** data and **retrieve** when needed
  * Data can be created, retrieved, updated and deleted (CRUD) from a table
* Rational database is a type of database that organizes data into tables and links them based on defined relationships
  * Allows to retrieve and combine data from one or more tables with a single query

* Repetitive data is problematic and makes the CRUD operations more challenging
  * Longer to go through data
  * Remove repetitive data across columns (**first normal form (1NF)**)
  * Remove repetitive data across rows (**second normal form (2NF)**)
* With separated tables, data can be retrieved by drawing meaningful links between the tables
  * Give each row a unique identifier (**primary key**)
    * Entire process is called **normalization**
      * Rows will appear in the database only once, which makes CRUD operations easier
* **Relational Database Management Systems (RDBMS)**
  * Software used to create and use relational databases (i.e. MySQL, SQLite and PostgreSQL)
    * SQLite: iOS and Android let developers manage their app's private databases
    * PostgreSQL: Useful for mapping applications
* **Structured Query Language (SQL)**
  * 

### ENTITY RELATIONSHIP DIAGRAM (ERD)
* Graphical representation of the data requirements for a database
  * **Entity**
    * Represents a person, palce or thing that you want to track in a database
    * Become a table in the database
    * Each occurrence of the entity is an 'entity instance'
      * Rows

  * **Attribute**
    * Describes various characteristics about an individual entity
      * Columns
      * Ex. First name

  * **Primary key**
    * An attribute or group of attributes that uniquely identifies an instance of the entity
      * No two rows have the same value
        * Ex. Student ID

  * **Relationship**
    * Describes how one or more entities interact with each other
    * A verb is often used to describe the relationship

  * **Cardinality**
    * The count of instances that are allowed or are necessary between entity relationships

* Crow's Foot Notation
!['Crow's Foot Notation Diagram'](https://res.cloudinary.com/practicaldev/image/fetch/s--Sf6yoYk6--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://i.ibb.co/qjw6dMn/Crow-Notation-Chart.png)

### SQL (STRUCTURED QUERY LANGUAGE)
* SQL is a programming language used to interact with relational databases

# **DAY 1 LECTURE NOTES**

## Third Tier of the Web Development Architecture
  * 3-Tier Architecture
    1. Client Tier
    2. Logic Tier
      * React, Node JS, etc.
    3. Data Tier
      * SQL, search engine, No SQL, etc.

  * Web browser is client to the web server
  * Web server is client to the database

## Relational Database
  * Data is broken down into tables with associations between them (relationships)
  * Each table is like a table (rows and columns)

## SQL (Structured Query Language)
  * DML (Data Manipulation Language)
    * Operations to manipulated the data
      * INSERT, UPDATE, DELETE, SELECT

## PSQL (PostgreSQL)
  * **psql -U postgres -h localhost -p 5433 spot**
    * -U: username
    * -h: localhost
    * -p: port number
      * default for PSQL is (5432)
      * (5433) included since it is different than the default port number
  * `\x` to toggle expanded view
  * To spread the command over multiple lines, do not include *;* at the end of the command
    * Can continue to write command next line
      * Include *;* to end the command

# **DAY 2 LECTURE NOTES** 

* User Stories / User Scenarios
  * Basic description of a feature
    * "As a (user/admin), I want to (_______)"
      * Ex. "As a user, I want to save a long_url and the app needs to create me a short-Url"
      * Ex. "As a user, I want to see all of my urls"
      * Ex. "As a user, I want to favourite some of my urls"
    * Database table typically expands from the noun of the user story
      * Ex. user, admin, url, etc.
* *Convention at LHL*
  * Plural table names
* `pgadmin4` for presenting tables
  * **Right click - Create ERD**
    * Can create ERD from data tables
    * Can create data tables from ERD

`Database`
* Users
  * username - varchar(150)
  * password - varchar(150)
  * email - varchar(150)
  * created_at - date/timestamp
* Urls
  * long_url - varchar(150)
  * short_url - varchar(7))
  * created_at - date/timestamp

`Relationship`
* **one-to-one**
  * Not typically used, but used for maintenance
  * Assigning admin user of all the users
* **one-to-many**
* **many-to-many**
  * not recommended
  * can fix by making a bridge table

# **DAY 2 COMPASS NOTES**

## Database Design

1. *Determine the purpose of the database*
    * This helps prepare for the remaining steps.

2. *Find and organize the information required*
    * Gather all of the types of information to record in the database, such as product name and order number.

3. *Divide the information into tables*
    * Divide information items into major entities or subjects, such as Products or Orders. Each subject then becomes a table.

4. *Turn information items into columns*
    * Decide what information needs to be stored in each table. Each item becomes a field, and is displayed as a column in the table. For example, an Employees table might include fields such as Last Name and Hire Date.

5. *Specify primary keys*
    * Choose each table's primary key. The primary key is a column, or a set of columns, that is used to uniquely identify each row. An example might be Product ID or Order ID.

6. *Set up the table relationships*
    * Look at each table and decide how the data in one table is related to the data in other tables. Add fields to tables or create new tables to clarify the relationships, as necessary.

7. *Refine the design*
    * Analyze the design for errors. Create tables and add a few records of sample data. Check if results come from the tables as expected. Make adjustments to the design, as needed.

8. *Apply the normalization rules*
    * Apply the data normalization rules to see if tables are structured correctly. Make adjustments to the tables, as needed.

## Database Normalization

* Database is normalized to reduce duplicate data
  * Organize data in the database
* Two things to consider:
  1. Internal redundancies
  2. Logically organized dependencies across different tables
* First normal form (1NF) demands every column and every field to contain only one value
  * Each row and column is unique

**One-to-Many Relationship**
1. What is one-to-many relationship?
  * One record in one table is related to many records in another table
    * Ex. one customer with many orders

2. Write a sentence
  * Ex. store the *customer information* and the *orders* that they have made

3. Write down the objects from the sentence
  * Identify words that describe the objects (i.e. nouns)
    * Ex. customer information, orders

4. Determine one-to-many relationship
  * Does object 1 have many object 2s, or does object 2 have many objects 1s
    * Ex. *Does a customer have many orders*, or does an order have many customers?
      * Customer-Order relationship is one-to-many

5. Create a diagram

6. Draw a line between the two tables

7. Add to diagram to describe one-to-many relationship

**Many-to-Many Relationship**
  * Make a bridge table between the two tables
    * Captures every instance of both tables

# **DAY 3 LECTURE NOTES** 

## Conneting Database to Node
* Node does not care what application we use for SQL
  * Install *node-postgres* for PSQL
    * https://node-postgres.com/features/connecting

```js
const { Pool, Client } = require('pg'); //to bring in Pool and Client keys

// protocol://user:password@host.database
const client = new Client {
  user: 'labber',
  host: 'localhost',
  database: 'LightBnB',
  password: 'labber',
  port: 5432,
}

client.connect(() => {
  console.log('Connected to the db');
});

const verb = process.argv[2]; //for command line argument
const id = process.argv[3]; // move outside switch statement since it is used multiple times
// `node file_name.js browse` to show the table
// `node file_name.js read 1` to read id 1

switch (verb) {
  case 'browse':
    client.query('SELECT * FROM primates;')
      .then((results) => {
        // console.log(results); //returns an object
        console.log(results.rows); //returns database tables in array, which is from results object
        client.end(); //to disconnect after the command
      })
    break;

  case 'read':
    // const id = process.argv[3];
    // client.query(`SELECT * FROM primates WHERE id = ${id};`) //this can be hacked by adding query after command
    //  SELECT * FROM primates WHERE id = 1; DROP TABLE primates; => deletes the table
    client.query(`SELECT * FROM primates WHERE id = $1;`, [id]) //to prevent hacking; $1 becomes a variable and placed in order as second parameter in array
    // node r read '1; DROP TABLE primates'
    //  SELECT * FROM primates WHERE id = '1; DROP TABLE primates'; => cannot delete the table
      .then((results) => {
        console.log(results.rows[0]); //[0] because results.rows only returns one row of array
        client.end();
      })
    break;
  
  case 'edit':
    const newName = process.argv[4];
    client.query(`UPDATE primates SET name = $1 WHERE id = $2;`, [newName, id]) //after update, data is not ordered
      .then(() => {
        console.log('primate has been updated');
        client.end();
      })
    break;

  case 'add':
    const species = process.argv[3];
    const name = process.argv[4];
    client.query(`INSERT INTO primates(species, name) VALUES($1, $2);`, [species, name])
      .then(() => {
        console.log('primate has been added');
        client.end();
      })
    break;

  case 'delete':
    client.query(`DELETE FROM primate WHERE id = $1;`, [id])
      .then(() => {
        console.log('primate has been removed from the table');
        client.end();
      })

  default:
    console.log('Enter a valid verb');
    client.end();
}
```

* `app.use(morgan('dev))` => lightweight logging

* `dotenv` npm
  * To keep sensitive information separately and not share with the world
  * declare `require('dotenv').config()` as early as possible
  * save `.env` file in node_modules folder
  * add `.env` in .gitignore file

# **DAY 3 COMPASS NOTES** 

## Data Definition Language (DDL)

* SQL commands used to define the database schema
  * i.e. CREATE, ALTER, DROP

## Data Manipulation Language (DML)

* SQL commands used to interact with data
  * i.e. SELECT, INSERT, UPDATE, DELETE

## Data Types

* SQL has many more data types than JS
  * SQL: SMALLINT, INTEGER, BIGINT, DECIMAL, NUMERIC, REAL, DOUBLE, SMALLSERIAL, SERIAL, BIGSERIAL
  * JS: number
* DBMS can be more efficient about storing data and can enforce rules about storing data

`Quick Reference`
* *Primary key column:*
  * Use the name id and then SERIAL PRIMARY KEY.
* *Foreign key columns:*
  * Add _id to the singular name of the column you are referencing.
  * If the primary key is SERIAL, then the foreign key should be INTEGER.
  * You also should create the foreign key with REFERENCES table_name(id) ON DELETE CASCADE.
* *Names, emails, usernames and passwords* can all be stored as VARCHAR(255). Students to cohorts would be cohort_id. The type would be INTEGER.
* *Dates* would use the DATE type. If we needed date and time, use TIMESTAMP.
* *Numbers:*
  * We will use INTEGER to represent most numbers. There are other sizes of integers as well.
  * SMALLINT -32,768 to 32,767 (thirty-two thousand)
  * INTEGER -2,147,483,648 to 2,147,483,647 (two billion)
  * BIGINT -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 (nine quintillion)
  * SERIAL 1 to 2,147,483,647 (auto incrementing)
* *Dates, Phone Numbers & Currency*
  * Become familiar with the ISO 8601 date formatting standard. The string '2018-02-12' uses this format to represent 'February 12th, 2018'. Year, month and then day. Dates should be stored consistently. Apply timezones and formatting when displayed to the user.
  * *Store phone numbers as VARCHAR*, there are so many possible formats. The number 214 748 3647 hits our INTEGER limit.
  * *Store currency as an integer representing cents*. Use a BIGINT if you need values over $21 million dollars.

## node-postgres
* npm library that allows to connect to PSQL database directly from node applications
* To use terminal to execute SQL queries, first connect to the database using a client app like psql
  * To connect to the *bootcampx database*, enter `psql bootcampx`
  * To connect to database in JS using `node-postgres`
    ```js
    const { Pool } = require('pg');

    const pool = new Pool({
      user: 'vagrant',
      password: '123',
      host: 'localhost',
      database: 'bootcampx'
    });
    ```
  * `pool.query` function accepts an SQL query as a JS string
    * The function then returns a promise that contains the result when the query is successful
    * Result outputs an object containing data
      * Data tables are contained in objects within an array in `rows` property
      * **Dealing with JS objects, not SQL/database**
    ```js
    pool.query(`
    SELECT id, name, cohort_id
    FROM students
    LIMIT 5;
    `)
    .then(res => {
      console.log(res);
    })
    .catch(err => console.log('query error', err.stack));
    ```
    
`Parameterized Query`
* **Always use parameterized queries when you have data that comes from an untrusted source, which is pretty much every source**
* Query broken down into 2 parts:
  1. Part that the developer writes and have complete control over (i.e. queryString)
  2. Part that comes from somewhere else and might be malicious such as user input (i.e. values)
* Avoid string concatenating parameters into the query text directly if passing parameters to the queries
  * Lead to SQL injection vulnerabilities
* `$` is a placeholder in the query that represents where a value should go but can't because it's coming from somewhere else (i.e. user input)
  * **$1, $2, ...** replaced with the data from array **[value1, value2, ...]**
  ```js
  const queryString = `
  SELECT students.id as student_id, students.name as name, cohorts.name as cohort
  FROM students
  JOIN cohorts ON cohorts.id = cohort_id
  WHERE cohorts.name LIKE $1
  LIMIT $2;
  `;

  const cohortName = process.argv[2];
  const limit = process.argv[3] || 5;
  // Store all potentially malicious values in an array.
  const values = [`%${cohortName}%`, limit];

  pool.query(queryString, values);
  ```
  