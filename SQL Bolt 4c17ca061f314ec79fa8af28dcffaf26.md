# SQL Bolt

# **Lesson 1:** SELECT Queries 101

## Guidelines

<aside>
💡 **Tip:**

Select query for all columns

```sql
SELECT *
FROM table_name;
```

</aside>

<aside>
💡 **Tip:**

Select query for a specific columns

```
SELECT column, another_column, …
FROM mytable;
```

</aside>

## Solutions

Exercise 1 — Tasks

- Find the **`title`** of each film

```sql
SELECT title FROM movies;
```

- Find the **`director`** of each film

```sql
SELECT director FROM movies;
```

- Find the **`title`** and **`director`** of each film

```sql
SELECT title,director FROM movies;
```

- Find the **`title`** and **`year`** of each film

```sql
SELECT title,year  FROM movies;
```

- Find **`all`** the information about each film

```sql
SELECT*FROM movies;
```

# **Lesson 2: Queries with constraints (Pt. 1)**

## Guidelines

<aside>
💡 **Tip:**

Select query with constraints

```sql
SELECT column, another_column, …
FROM mytable
WHERE condition
    AND/OR another_condition
    AND/OR …;
```

</aside>

<aside>
💡 **Tip:**

More complex clauses can be constructed by joining numerous **`AND`** or **`OR`** logical keywords

| Operator | Condition |
| --- | --- |
| =, !=, < <=, >, >= | Standard numerical operators |
| BETWEEN … AND … | Number is within range of two values (inclusive) |
| NOT BETWEEN … AND … | Number is not within range of two values (inclusive) |
| IN (…) | Number exists in a list |
| NOT IN (…) | Number does not exist in a list |
</aside>

## Solutions

Exercise 2 — Tasks

- Find the movie with a row **`id`** of 6

```sql
SELECT title FROM movies 
WHERE id = 6;
```

- Find the movies released in the **`year`**s between 2000 and 2010

```sql
SELECT title FROM movies 
WHERE year BETWEEN 2000 AND 2010 ;
```

- Find the movies **not** released in the **`year`**s between 2000 and 2010

```sql
SELECT title FROM movies 
WHERE year NOT BETWEEN 2000 AND 2010 ;
```

- Find the first 5 Pixar movies and their release **`year`**

```sql
SELECT title , year
FROM movies 
LIMIT 5 ;
```

# **Lesson 3: Queries with constraints (Pt. 2)**

## Guidelines

<aside>
💡 **Tip:**

Select query with constraints

```sql
SELECT column, another_column, …
FROM mytable
WHERE condition
    AND/OR another_condition
    AND/OR …;
```

</aside>

<aside>
💡 **Tip:**

few common T**ext-Data** specific operators below

| Operator | Condition |
| --- | --- |
| = | Case sensitive exact string comparison |
| != or <> | Case sensitive exact string inequality comparison |
| LIKE | Case insensitive exact string comparison |
| NOT LIKE | Case insensitive exact string inequality comparison |
| % | Used anywhere in a string to match a sequence of zero or more characters (only with LIKE or NOT LIKE) |
| _ | Used anywhere in a string to match a single character (only with LIKE or NOT LIKE)  |
| IN (…) | String exists in a list |
| NOT IN (…) | String does not exist in a list |
</aside>

## Solutions

Exercise 3 — Tasks

- Find all the Toy Story movies

```sql
SELECT * 
FROM movies
WHERE title LIKE "Toy Story%";
```

- Find all the movies directed by John Lasseter

```sql
SELECT * 
FROM movies
WHERE director = 'John Lasseter';
```

- Find all the movies (and director) not directed by John Lasseter

```sql
SELECT title,director 
FROM movies
WHERE NOT director = 'John Lasseter';
```

- Find all the WALL-* movies

```sql
SELECT *
FROM movies
WHERE title LIKE 'WALL_%';
```

# ****Lesson 4: Filtering and sorting Query results****

## Guidelines

<aside>
💡 **Tip:**

Select query with unique results

```sql
SELECT DISTINCT column, another_column, …
FROM mytable
WHERE condition(s);
```

</aside>

<aside>
💡 **Ordering results:**

Select query with ordered results

```sql

SELECT column, another_column, …
FROM mytable
WHERE condition(s)
ORDER BY column ASC/DESC;
```

</aside>

<aside>
💡 **Limiting results to a subset:**

Select query with limited rows

```sql
SELECT column, another_column, …
FROM mytable
WHEREcondition(s)ORDER BY column ASC/DESC
LIMIT num_limit OFFSET num_offset;
```

</aside>

<aside>
💡 **HINT**:

The **`LIMIT`** will reduce the number of rows to return, and the optional **`OFFSET`** will specify where to begin counting the number rows from.

</aside>

## Solutions

Exercise 4 — Tasks

- List all directors of Pixar movies (alphabetically), without duplicates

```sql
SELECT DISTINCT director
FROM movies
ORDER BY director ASC;
```

- List the last four Pixar movies released (ordered from most recent to least)

```sql
SELECT title,year
FROM movies
ORDER BY year DESC
LIMIT 4;
```

- List the **first** five Pixar movies sorted alphabetically

```sql
SELECT title
FROM movies
ORDER BY title ASC
LIMIT 5;
```

- List the **next** five Pixar movies sorted alphabetically

```sql
SELECT title
FROM movies
ORDER BY title ASC
LIMIT 5
OFFSET 5 ;
```

# **SQL Review: Simple SELECT Queries**

## Guidelines

<aside>
💡 **Tip:**

SELECT query

```sql
SELECT column, another_column, …
FROM mytable
WHEREcondition(s)ORDER BY column ASC/DESC
LIMIT num_limit OFFSET num_offset;
```

</aside>

## **Exercise**

Review 1 — Table: Most Populous Cities of North America

- List all the Canadian cities and their populations

```sql
SELECT City ,Population
FROM north_american_cities
WHERE Country = 'Canada';
```

- Order all the cities in the United States by their latitude from north to south

```sql
SELECT City 
FROM north_american_cities
WHERE Country = 'United States'
ORDER BY latitude DESC;
```

- List all the cities west of Chicago, ordered from west to east

```sql
SELECT * 
FROM north_american_cities
WHERE Longitude < (SELECT Longitude FROM north_american_cities WHERE City = 'Chicago')
ORDER BY Longitude ASC;
```

- List the two largest cities in Mexico (by population)

```sql
SELECT City 
FROM north_american_cities
WHERE Country = 'Mexico'
ORDER BY population DESC
LIMIT 2
;
```

- List the third and fourth largest cities (by population) in the United States and their population

```sql
SELECT City 
FROM north_american_cities
WHERE Country = 'United States'
ORDER BY population DESC
LIMIT 2
OFFSET 2
;
```

# **Lesson 6: Multi-table queries with JOINs**

## Guidelines

<aside>
💡 **Multi-table queries with JOINs:**

Select query with INNER JOIN on multiple tables

```sql
SELECT column, another_table_column, …
FROM mytable
INNER JOIN another_table
    ON mytable.id = another_table.idWHEREcondition(s)ORDER BY column, … ASC/DESC
LIMIT num_limit OFFSET num_offset;
```

</aside>

## **Exercise**

Exercise 6 — Tasks

- Find the domestic and international sales for each movie

```sql
SELECT title,b.Domestic_sales,b.International_sales
FROM movies m , Boxoffice b
WHERE m.id = b.Movie_id ;
```

- Show the sales numbers for each movie that did better internationally rather than domestically

```sql
SELECT title,b.Domestic_sales,b.International_sales
FROM movies m , Boxoffice b
WHERE m.id = b.Movie_id AND b.Domestic_sales<b.International_sales;
```

- List all the movies by their ratings in descending order

```sql
SELECT title,Rating
FROM movies m , Boxoffice b
WHERE m.id = b.Movie_id 
ORDER BY Rating DESC ;
```

# ****Lesson 7: OUTER JOINs****

## Guidelines

![joins.jpg](SQL%20Bolt%204c17ca061f314ec79fa8af28dcffaf26/joins.jpg)

<aside>
💡 **Multi-table queries with JOINs:**

Select query with LEFT/RIGHT/FULL JOINs on multiple tables

```sql
SELECT column, another_column, …
FROM mytable
INNER/LEFT/RIGHT/FULL JOIN another_table
    ON mytable.id = another_table.matching_idWHEREcondition(s)ORDER BY column, … ASC/DESC
LIMIT num_limit OFFSET num_offset;
```

</aside>

## **Exercise**

Exercise 7 — Tasks

- Find the list of all buildings that have employees

```sql
SELECT DISTINCT Building
FROM employees;
```

- Find the list of all buildings and their capacity

```sql
SELECT *
FROM Buildings ;
```

- List all buildings and the distinct employee roles in each building (including empty buildings)

```sql
SELECT Distinct Building_name , e.Role
FROM Buildings b
LEFT JOIN Employees e 
    ON b.Building_name = e.Building;
```

# ****Lesson 8: A short note on NULLs****

## Guidelines

<aside>
💡 **Notice:**

An alternative to **`NULL`** values in your database is to have ***data-type appropriate default values***, like 0 for numerical data, empty strings for text data, etc. But if your database needs to store incomplete data, then **`NULL`** values can be appropriate if the default values will **skew** later analysis (for example, when taking averages of numerical data).

</aside>

<aside>
💡 **Multi-table queries with JOINs:**

Select query with constraints on NULL values

```sql
SELECT column, another_column, …
FROM mytable
WHERE column IS/IS NOT NULLAND/ORanother_conditionAND/OR …;
```

</aside>

## **Exercise**

Exercise 8 — Tasks

- Find the name and role of all employees who have not been assigned to a building

```sql
SELECT name,role
FROM employees
WHERE Building IS NULL ;
```

- Find the names of the buildings that hold no employees

```sql
SELECT Building_name
FROM Buildings b
LEFT JOIN Employees e
    ON b.Building_name = e.Building
WHERE e.role IS NULL ;
```

# ****Lesson 9: Queries with expressions****

## Guidelines

<aside>
💡 **Notice:**

Example query with expressions

```sql
SELECTparticle_speed / 2.0 AS half_particle_speed
FROM physics_data
WHERE ABS(particle_position) * 10.0 > 500;
```

</aside>

<aside>
💡 **Aliases:**

Select query with expression aliases

```sql
SELECT col_expression AS expr_description, …
FROM mytable;
```

</aside>

## **Exercise**

Exercise 9 — Tasks

- List all movies and their combined sales in **millions** of dollars

```sql
SELECT m.Title ,(b.Domestic_sales + b.International_sales)/1000000 AS sales
FROM movies m ,Boxoffice b
WHERE m.Id = b.Movie_id;
```

- List all movies and their ratings **in percent**

```sql
SELECT m.Title ,ROUND(b.Rating*10)
FROM movies m ,Boxoffice b
WHERE m.Id = b.Movie_id;
```

- List all movies that were released on even number years

```sql
SELECT m.Title ,year
FROM movies m ,Boxoffice b
WHERE m.Id = b.Movie_id
AND year%2 = 0;
```

# ****Lesson 10: Queries with aggregates (Pt. 1)****

## Guidelines

<aside>
💡 **Notice:**

Select query with aggregate functions over all rows

```sql
SELECT AGG_FUNC(column_or_expression) AS aggregate_description, …
FROM mytable
WHERE constraint_expression;
```

</aside>

<aside>
💡 **Aggregation Functions:**

| Function | Description |
| --- | --- |
| COUNT(*), COUNT(column) | A common function used to counts the number of rows in the group if no column name is specified. Otherwise, count the number of rows in the group with non-NULL values in the specified column. |
| MIN(column) | Finds the smallest numerical value in the specified column for all rows in the group. |
| MAX(column) | Finds the largest numerical value in the specified column for all rows in the group. |
| AVG(column) | Finds the average numerical value in the specified column for all rows in the group. |
| SUM(column) | Finds the sum of all numerical values in the specified column for the rows in the group. |
</aside>

<aside>
💡 **Grouped aggregate functions:**

Select query with aggregate functions over groups

```sql
SELECT AGG_FUNC(column_or_expression) AS aggregate_description, …
FROM mytable
WHERE constraint_expression 
GROUP BY column;
```

</aside>

## **Exercise**

Exercise 10 — Tasks

- Find the longest time that an employee has been at the studio

```sql
SELECT MAX(Years_employed)
FROM employees;
```

- For each role, find the average number of years employed by employees in that role

```sql
SELECT role, AVG(Years_employed)
FROM employees
GROUP BY role;
```

- Find the total number of employee years worked in each building

```sql
SELECT  Building,SUM(Years_employed)
FROM employees
GROUP BY Building;
```

# ****Lesson 11: Queries with aggregates (Pt. 2)****

## Guidelines

<aside>
💡 **HAVING Clause:**

Select query with HAVING constraint

```sql
SELECT group_by_column, AGG_FUNC(column_expression) AS aggregate_result_alias, …
FROM mytable
WHEREconditionGROUP BY column
HAVINGgroup_condition;
```

</aside>

## **Exercise**

Exercise 11 — Tasks

- Find the number of Artists in the studio (without a **HAVING** clause)

```sql
SELECT role ,COUNT(name)
FROM employees
WHERE role = 'Artist';
```

- Find the number of Employees of each role in the studio

```sql
SELECT role ,COUNT(name)
FROM employees
GROUP BY role;
```

- Find the total number of years employed by all Engineers

```sql
SELECT role ,SUM(Years_employed)
FROM employees
WHERE role = 'Engineer';
```

# ****Lesson 12: Order of execution of a Query****

## Guidelines

<aside>
💡 **Complete SELECT Query:**

```sql
SELECT DISTINCT column, AGG_FUNC(column_or_expression), …
FROM mytable
    JOIN another_table
      ON mytable.column = another_table.column
    WHEREconstraint_expressionGROUP BY column
    HAVINGconstraint_expressionORDER BYcolumn ASC/DESC
    LIMITcount OFFSETCOUNT;
```

</aside>

<aside>
💡 **Query order of Execution:**

![order.png](SQL%20Bolt%204c17ca061f314ec79fa8af28dcffaf26/order.png)

</aside>

## **Exercise**

Exercise 12 — Tasks

- Find the number of movies each director has directed

```sql
SELECT director , count(title)
FROM movies
GROUP BY director;
```

- Find the total domestic and international sales that can be attributed to each director

```sql
SELECT director , SUM(Domestic_sales+International_sales) as sales
FROM movies m , Boxoffice  b
WHERE m.id = b.movie_id
GROUP BY director;
```

# ****Lesson 13: Inserting rows****

## Guidelines

<aside>
💡 **What is a Schema?**

In SQL, the `database schema` is what describes the structure of each table, and the datatypes that each column of the table can contain.

</aside>

<aside>
💡 **Inserting new data:**

Insert statement with values for all columns

```sql
INSERT INTO mytable
VALUES (value_or_expr, another_value_or_expr, …),
       (value_or_expr_2, another_value_or_expr_2, …),
       …;
```

Insert statement with specific columns

```sql
INSERT INTO mytable
(column, another_column, …)
VALUES (value_or_expr, another_value_or_expr, …),
      (value_or_expr_2, another_value_or_expr_2, …),
      …;
```

</aside>

## **Exercise**

Exercise 13 — Tasks

- Add the studio's new production, **Toy Story 4** to the list of movies (you can use any director)

```sql
INSERT INTO Movies 
VALUES (4, 'Toy Story 4','dd',2020,90);
```

- Find the total domestic and international sales that can be attributed to each director

```sql
INSERT INTO BoxOffice  
VALUES (4, 8.7,340000000,270000000);
```

# ****Lesson 14: Updating rows****

## Guidelines

<aside>
💡 **Query:**

Update statement with values

```sql
UPDATE mytable
SET column = value_or_expr,
other_column = another_value_or_expr,
…
WHERE condition;
```

</aside>

## **Exercise**

Exercise 14 — Tasks

- The director for A Bug's Life is incorrect, it was actually directed by **John Lasseter**

```sql
UPDATE Movies
SET Director = 'John Lasseter'
WHERE title = "A Bug's Life";
```

- The year that Toy Story 2 was released is incorrect, it was actually released in **1999**

```sql
UPDATE Movies
SET year = 1999
WHERE title = "Toy Story 2";
```

- Both the title and director for Toy Story 8 is incorrect! The title should be "Toy Story 3" and it was directed by **Lee Unkrich**

```sql
UPDATE Movies
SET title = "Toy Story 3" , director = 'Lee Unkrich'
WHERE title = "Toy Story 8";
```

# ****Lesson 15: Deleting rows****

## Guidelines

<aside>
💡 **Query:**

Delete statement with condition

```sql
DELETE FROM mytable
WHERE condition;
```

</aside>

## **Exercise**

Exercise 15 — Tasks

- This database is getting too big, lets remove all movies that were released **before** 2005.

```sql
DELETE FROM Movies
WHERE year < 2005;
```

- Andrew Stanton has also left the studio, so please remove all movies directed by him.

```sql
DELETE FROM Movies
WHERE director = 'Andrew Stanton';
```

# ****Lesson 16: Creating tables****

## Guidelines

<aside>
💡 **Query:**

Create table statement w/ optional table constraint and default value

```sql
CREATE TABLE IF NOT EXISTS mytable (
    column *DataType* TableConstraint DEFAULT default_value,
    another_column *DataType* TableConstraint DEFAULT default_value,
    …
);
```

</aside>

<aside>
💡 **Table data types:**

Create table statement w/ optional table constraint and default value

| Data type | Description |
| --- | --- |
| INTEGER, BOOLEAN | The integer datatypes can store whole integer values like the count of a number or an age. In some implementations, the boolean value is just represented as an integer value of just 0 or 1. |
| FLOAT, DOUBLE, REAL | The floating point datatypes can store more precise numerical data like measurements or fractional values. Different types can be used depending on the floating point precision required for that value. |
| CHARACTER(num_chars), VARCHAR(num_chars), TEXT | The text based datatypes can store strings and text in all sorts of locales. The distinction between the various types generally amount to underlaying efficiency of the database when working with these columns.
Both the CHARACTER and VARCHAR (variable character) types are specified with the max number of characters that they can store (longer values may be truncated), so can be more efficient to store and query with big tables. |
| DATE, DATETIME | SQL can also store date and time stamps to keep track of time series and event data. They can be tricky to work with especially when manipulating data across timezones. |
| BLOB | Finally, SQL can store binary data in blobs right in the database. These values are often opaque to the database, so you usually have to store them with the right metadata to requery them. |
</aside>

<aside>
💡 **Table Constraints:**

| Constraint | Description |
| --- | --- |
| PRIMARY KEY | This means that the values in this column are unique, and each value can be used to identify a single row in this table. |
| AUTOINCREMENT | For integer values, this means that the value is automatically filled in and incremented with each row insertion. Not supported in all databases. |
| UNIQUE | This means that the values in this column have to be unique, so you can't insert another row with the same value in this column as another row in the table. Differs from the `PRIMARY KEY` in that it doesn't have to be a key for a row in the table. |
| NOT NULL | This means that the inserted value can not be `NULL`. |
| CHECK (expression) | This allows you to run a more complex expression to test whether the values inserted are valid. For example, you can check that values are positive, or greater than a specific size, or start with a certain prefix, etc. |
| FOREIGN KEY | This is a consistency check which ensures that each value in this column corresponds to another value in a column in another table.For example, if there are two tables, one listing all Employees by ID, and another listing their payroll information, the `FOREIGN KEY` can ensure that every row in the payroll table corresponds to a valid employee in the master Employee list. |
</aside>

## **Exercise**

Exercise 16 — Tasks

1. Create a new table named **`Database`** with the following columns:This table has no constraints.
    
    – **`Name`** A string (text) describing the name of the database
    
    – **`Version`** A number (floating point) of the latest version of this database
    
    – **`Download_count`** An integer count of the number of times this database was downloaded
    

```sql
CREATE TABLE database (
   
    name TEXT,
    Version  FLOAT,
    Download_count INTEGER
    
);
```

# ****Lesson 17: Altering tables****

## Guidelines

<aside>
💡 **Adding columns:**

```sql
ALTER TABLE mytable
ADD column DataType OptionalTableConstraint 
    DEFAULT default_value;
```

</aside>

<aside>
💡 **Removing columns:**

```sql
ALTER TABLE mytable
DROP column_to_be_deleted;
```

</aside>

<aside>
💡 **Renaming the table:**

```sql
ALTER TABLE mytable
RENAME TO new_table_name;
```

</aside>

## **Exercise**

Exercise 17 — Tasks

- Add a column named **Aspect ratio** with a **FLOAT** data type to store the aspect-ratio each movie was released in.

```sql
ALTER TABLE movies
ADD Aspect_ratio FLOAT;
```

- Add another column named **Language** with a **TEXT** data type to store the language that the movie was released in. Ensure that the default for this language is **English**.

```sql
ALTER TABLE movies
ADD Language  TEXT DEFAULT  English ;
```

# ****Lesson 18: Dropping tables****

## Guidelines

<aside>
💡 **Query:**

Drop table statement

```sql
DROP TABLE IF EXISTS mytable;
```

</aside>

## **Exercise**

Exercise 18 — Tasks

- We've sadly reached the end of our lessons, lets clean up by removing the **Movies** table

```sql
DROP TABLE IF EXISTS Movies ;
```

- And drop the **Box Office** table as well

```sql
DROP TABLE IF EXISTS BoxOffice  ;
```