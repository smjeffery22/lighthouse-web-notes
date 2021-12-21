
CREATE TABLE tablename (title1 DATA TYPE PRIMARY KEY, title2 DATA TYPE, title3 DATA TYPE, ...)
  * Data type: TEXT, NUMERIC, INTEGER, REAL, NONE

INSERT INTO tablename VALUES ('title1', 'item to insert in title2', 'item to insert in title3, ...)

SELECT title FROM tablename WHERE (comparison operators) ORDER BY item
  * SELECT * selects all items
  * WHERE to filter results out
  * ORDER BY (default ascending)
    * ORDER BY column1, column2, ... ASC|DESC;

SELECT SUM(title) FROM tablename
SELECT title SUM(title) FROM tablename GROUP BY title
  * Aggregate function to get max, min, sum, average, etc. in database
  * Group the result from aggregate function by specific item

`SELECT DISTINCT:` To retrieve the only distinct values in a specified list of columns

`IN:` To check if an item is in a list
* SELECT name, population FROM world
  * WHERE name IN ('Sweden', 'Norway', 'Denmark');
* Also can be used as boolean values
  * Either 0 or 1 will be assigned to above values when SELECTed if exists

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

`<>:` **Not equals** operator

`HAVING:` Allows to filter the groups which are displayed, after the aggrgation
  * Aggregations are SUM, COUNT, MIN, MAX and AVG

`WHERE:` Filters rows before the aggregation

`LIMIT:` Limit the number of records returned based on a limit value