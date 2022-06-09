# SQL (STRUCTURED QUERY LANGUAGE)

`CREATE TABLE` tablename (title1 DATA TYPE/SERIAL PRIMARY KEY, title2 DATA TYPE, title3 DATA TYPE, ...)
  * title1 is typically id
  * Data type: TEXT, VARCHAR(#), NUMERIC, INTEGER, REAL, DATE, NONE
    * Include **NOT NULL** after datatype to not accept NULL
  * PRIMARY KEY **AUTOINCREMENT** to increment id number automatically when inserting data
    * **SERIAL** autoincrements id
    *  *id SERIAL PRIMARY KEY = id INTEGER PRIMARY KEY AUTOINCREMENT*
  * **Foreign Key** is a column or a group of columns in a table that reference the primary key of another table
    * Table that contains the foreign key is called the referencing/child table
    * Table referenced by the foreign key is called the referenced/parent table
    * **REFERENCE** to reference *parent_table(primary key)*
    * **ON DELETE CASADE** to specify whether the row should be deleted in a child table when corresponding row in the parent table is deleted
      ```sql
      [CONSTRAINT fk_name]
        FOREIGN KEY(fk_columns) 
        REFERENCES parent_table(parent_key_columns)
      [ON DELETE delete_action]
      [ON UPDATE update_action]

      CREATE TABLE pets (
      id SERIAL PRIMARY KEY,
      name VARCHAR(255) NOT NULL,
      owner_id INTEGER NOT NULL REFERENCES users(id) ON DELETE CASCADE
      );
      ```
  * **DEFAULT value** at the end of the column declaration line to set default value
      ```sql
      CREATE TABLE properties (
      id SERIAL PRIMARY KEY NOT NULL,
      owner_id INTEGER REFERENCES users(id) ON DELETE CASCADE,
      number_of_bathrooms INTEGER NOT NULL DEFAULT 0,
      number_of_bedrooms INTEGER NOT NULL DEFAULT 0,
      active BOOLEAN NOT NULL DEFAULT TRUE
      )
      ```

INSERT INTO tablename VALUES ('title1', 'item to insert in title2', 'item to insert in title3, ...)
  * INSERT INTO tablename(title2, title3, title4, title5) VALUES (item2, item3, item4, item5)
    * If primary key is autoincremented

SELECT title FROM tablename WHERE (comparison operators) ORDER BY item
  * SELECT * selects all items
  * WHERE to filter results out
  * `ORDER BY` (default ascending)
    * ORDER BY column1, column2, ... ASC|DESC;

SELECT SUM(title) FROM tablename
SELECT title SUM(title) FROM tablename **GROUP BY** title
  * Aggregate function to get max, min, sum, average, etc. in database
  * **GROUP BY** Group the result from aggregate function by specific item
    * Allows to combine the results based on a column so an aggregate can be applied to each group
    * Can use alias from the SELECT attribute as GROUP BY is evaluated after aggregate

`SELECT DISTINCT:` To retrieve the only distinct values in a specified list of columns

`COUNT():` Count the **number of rows**
* COUNT(*) simply returns the number of rows
* COUNT(address) counts the number of non-null addresses in the result set.
* Finally, COUNT(DISTINCT address) counts the number of different addresses in the facilities table.

`AVG() & SUM()` Average & total sum of a **numeric column**

`IN:` To check if an item is in a list
* SELECT name, population FROM world
  * WHERE name IN ('Sweden', 'Norway', 'Denmark');
* Also can be used as boolean values
  * Either 0 or 1 will be assigned to above values when SELECTed if exists

`NOT IN:` Opposite of 'IN'

`BETWEEN:` Allows range checking (inclusive of boundary values)
* SELECT name, area FROM world
  * WHERE area BETWEEN 200000 AND 250000

`LIKE:` Used in a WHERE clause to search for a specified pattern in a column
* The percent sign (%) represents zero, one, or multiple characters
  * WHERE name LIKE "Al%"
    * Start with Al
  * WHERE name LIKE "%al"
    * End with al
  * WHERE name LIKE "%al%"
    * al in any position
* The underscore sign (_) represents one, single character
  * WHERE name LIKE "_a%"
    * a in the second position
  * WHERE name LIKE "a_%"
    * Start with a and at least 2 characters in length
* Using multiple LIKE statements
  * WHERE name LIKE '%a%' AND name LIKE'%e%' AND name LIKE'%i%' AND name LIKE'%o%' AND name LIKE'%u%'

`NOT LIKE:` Opposite of LIKE, to exclude characters from the results

`REGEXP:` Pattern matching operation similar to LIKE
* '^A': beginning of string
* 'a%': end of string
* '[...]'	Any character listed between the square brackets
  * 'p1|p2|p3'	Alternation; matches any of the patterns p1, p2, or p3
* '[^...]'	Any character not listed between the square brackets
* Ex.
  * SELECT name FROM person_tbl WHERE name REGEXP '^st';
  * SELECT name FROM person_tbl WHERE name REGEXP 'ok$';
  * SELECT name FROM person_tbl WHERE name REGEXP 'mar';
  * SELECT name FROM person_tbl WHERE name REGEXP 'mar|may';

`XOR:` Exclusive OR
  * WHERE area > 3000000 XOR population > 250000000
    * **Excludes** items that meet the above conditions

`ROUND:` Round number
  * ROUND(population/1000000, 2)
  * ROUND(population/1000000, -3)
    * Negative number indicates rounding to integer (-3 => round to nearest 1000)

`LENGTH:` Length of an item
  * LENGTH(name)

`LEFT(s, n):` To extract n characters from the start of the string s
  * LEFT('Hello world', 4) -> 'Hell'     

`<> and !=:` **Not equals** operator, where '!=' is not ISO standard

`HAVING:` Allows to filter the groups which are displayed, after the aggrgation
  * Aggregations are SUM, COUNT, MIN, MAX and AVG
  * Playing with grouped values
    * Comes after GROUP BY
  * Evaluated before the SELECT attribute so cannot use the alias from the SELECT

`WHERE:` Filters rows before the aggregation

`LIMIT:` Limit the number of records returned based on a limit value

`AS:` To rename the column title
  * SUM(title) AS New_Title

`CASE:` To add a new column
  * Similar to if/switch statement
  * Simple syntax:
    ```sql
    CASE input_expression   
        WHEN when_expression THEN result_expression [ ...n ]   
        [ ELSE else_result_expression ]   
    END
    ```
  * Ex.
    ```sql
    SELECT COUNT(*),
        CASE 
            WHEN heart_rate > 220-30 THEN 'above max'
            WHEN heart_rate > ROUND(0.90 * (220-30)) THEN 'above target'
            WHEN heart_rate > ROUND(0.50 * (220-30)) THEN 'within target'
            ELSE 'below target'
        END as hr_zone // to end CASE statement and rename the column title
    FROM exercise_logs
    GROUP BY hr_zone;
    ```

`JOIN:` Combine rows from two or more tables based on a related column between them
* SELECT * FROM game JOIN goal ON (id=matchid)
  * JOIN: merge data from goal table with that from the game table using
    * Above syntax is INNER JOIN (JOIN can be replaced by INNER JOIN)
      * **INNER JOIN** returns rows where there is a match between two tables
        * Row **will not appear** in the results if the foreign key is **NULL**
    * **LEFT/RIGHT/FULL OUTER JOIN** returns rows regardless of the condition being met
      * LEFT for the table written to the left of JOIN
      * RIGHT for the table written to the right of JOIN
      * FULL for both tables
  * ON: how to figure out which rows in game table go with which rows in goal table
    * ON (game.id = goal.matchid) is more specific
    * **Every JOIN must have ON**
* **Order of attributes** in syntax
  * **WHERE > GROUP BY > HAVING > ORDER**

`UNION:` Combine the results of two SQL queries into a single table
* Both results from the two queries must have the same number of columns and compatible data types
* Removes duplicate rows, whereas *UNION ALL* does not
  ```sql
  SELECT surname 
  FROM cd.members
  UNION 
  SELECT name FROM cd.facilities
  ```

`Nested SELECT`
* **As a Column in SELECT**
  * SELECT can be nested inside SELECT if the query returns a single value
    ```sql
    SELECT (
      SELECT count(assignments)
      FROM assignments
    ) - count(assignment_submissions) as total_incomplete
    FROM assignment_submissions
    JOIN students ON students.id = student_id
    WHERE students.name = 'Ibrahim Schimmel';
    ```
* **FROM Sub Select Table**
  * Result of a SELECT is effectively a table that can be used like a table
  * 'as totals_table' gives an alias to the subquery so that its name can be used like any other table
    * 'avg(total_students)' <=> 'avg(totals_table.total_students)'
    ```sql
    SELECT avg(total_students) as average_students
    FROM (
      SELECT count(students) as total_students
      FROM students
      JOIN cohorts on cohorts.id = cohort_id
      GROUP BY cohorts
    ) as totals_table;
    ```
* **WHERE and Search Within a Result Set IN**
  * Use with WHERE
    ```sql
    SELECT assignments.name
    FROM assignments 
    WHERE id NOT IN
    (
      SELECT assignment_id
      FROM assignment_submissions
      JOIN students ON students.id = student_id
      WHERE students.name = 'Ibrahim Schimmel'
    );
    ```

`ROUND` / `CONCAT`
```sql
ROUND(number, decimal_places) => ROUND(123.45, 0)
CONCAT(s1, s2, ...) => CONCAT(region, name, '%') <=> regionname%
```

# PSQL (PostgreSQL)

`CREATE DATABASE` database_name
  * Create a new database
  * **\c database_name** to start using the database
    * Prompt **database_name=#** indicates that the database is being used

## Terms
`entities` Each table
`queries` Request for data/information from a database table or combination of tables using SQL statements

## Commands
  * `\l` Lists database
  * `\i filename` Reads input from the file 'filename' and executes it as though it had been typed on the keyboard
    * Create .sql file and save SQL codes to execute in the file
    * Use \i command to execute the saved SQL codes
    * Run psql inside the project folder and use \i command
  * `\dt` Lists all tables in PSQL database
  * `\d` to show the schema of a table
    * Shows column and data type
  * `\x` to change table view
  * `DROP TABLE table_name` Deletes the table
    * `DROP TABLE table_name CASCADE` Adding CASCADE also deletes other tables that depend on table_name
    * `DROP TABLE IF EXISTS table_name CASCADE` To make sure the table exists before dropping it

### Altering Table
  * Add/remove a column
  * Change an existing column type
  * Add/remove an index

```sql
ALTER TABLE table_name action
```

  * `action:`
    * `ADD COLUMN` to add a column
      ```sql
      ALTER TABLE table_name 
      ADD COLUMN column_name datatype column_constraint;
      ```
    * `DROP COLUMN` to delete a column
      ```sql
      ALTER TABLE table_name 
      DROP COLUMN column_name;
      ```
    * `RENAME COLUMN TO` to rename a column
      ```sql
      ALTER TABLE table_name 
      RENAME COLUMN column_name 
      TO new_column_name;
      ```
    * `ALTER COLUMN [SET DEFAULT | DROP DEFAULT]` to change a default value of a column
      ```sql
      ALTER TABLE table_name 
      ALTER COLUMN column_name 
      [SET DEFAULT value | DROP DEFAULT];
      ```
    * `ALTER COLUMN [SET NOT NULL | DROP NOT NULL]` to change NOT NULL constraint
      ```sql
      ALTER TABLE table_name 
      ALTER COLUMN column_name 
      [SET NOT NULL | DROP NOT NULL];
      ```
    * `RENAME TO` to rename a table
      ```sql
      ALTER TABLE table_name 
      RENAME TO new_table_name;
      ```

### Inserting into Table
  * Insert a new row into a table
  * If a row is added to a table and a value is not included for a column, that value is NULL
    * Include NOT NULL after datat type to require a value

```sql
INSERT INTO table_name(column1, column2, …) 
VALUES (value1, value2, …),
(value1, value2, …);
```

### Deleting Data from Table
  * Delete one or more row(s) from a table

```sql
DELETE FROM table_name
WHERE condition;
```

### Updating Data in Table
  * Modify data in a table

```sql
UPDATE table_name
SET column1 = value1,
    column2 = value2,
    ...
WHERE condition;
```