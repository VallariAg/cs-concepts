# Postgresql

Course: https://www.udemy.com/course/sql-and-postgresql/ 

## Basic SQL Recap

Playground: https://pg-sql.com/ 

SQL statements:

1. Create table 
    
    `CREATE TABLE` - keyword, `cities` - identifier 
    
    ```sql
    CREATE TABLE cities (
    	name VARCHAR(50),
      country VARCHAR(50),
      population INTEGER,
      area INTEGER
    );
    ```
    
2. Insert data in table
    
    column names order should match order of values
    
    ```sql
    INSERT INTO cities (name, country, population, area) 
    VALUES 
    	('Delhi', 'India', 28505000, 2240), 
    	('Shanghai', 'China', 22505000, 4015); 
    ```
    
3. query data
    
    ```sql
    SELECT * FROM cities;
    SELECT name, country FROM cities;
    SELECT name, name, name FROM cities;
    ```
    
4. update records
    
    ```sql
    UPDATE cities SET population = 39505000 WHERE name = 'Tokyo';
    ```
    
5. delete record
    
    ```sql
    DELETE FROM cities WHERE name = 'Tokyo';
    ```
    

Calculated columns:  

1. integers: `*`   `/`   `+`   `-`
    
    `%` (remainder) `@` (absolute) `^` (exponent) 
    
    ```sql
    SELECT name, population / area FROM cities;   -- new column name: ?column?
    SELECT name, population / area AS density FROM cities;
    ```
    
2. string operations on columns:
    
    `||`  (join) `CONCAT()` (join) `LOWER()`  `UPPER()` `LENGHT()`
    
    ```sql
    SELECT name || country AS location FROM cities;
    SELECT name || ', ' || country AS location FROM cities;
    
    SELECT CONCAT(name, ', ' , country) AS location FROM cities;
    
    SELECT CONCAT(UPPER(name), ', ', UPPER(country)) AS location FROM cities;
    SELECT UPPER(CONCAT(name, ', ', country)) AS location FROM cities;
    ```
    

Filtering Records:

1. `WHERE` 
    
    postgres SQL process order: `FROM cities` → `WHERE area > 4000` → `SELECT name`
    
    ```sql
    SELECT name, area FROM cities WHERE area > 4000;
    ```
    
    `=` is not assignment, It is comparison parameter for equality.
    
    `<>`  or `!=` → not equal check
    
    `IN`  (), `BETWEEN` (), `NOT IN` ()
    
    ```sql
    SELECT name, area FROM cities WHERE area = 8223;  -- equal check
    
    SELECT name, area FROM cities WHERE area <> 8223; -- not equal check
    
    SELECT name, area FROM cities WHERE area BETWEEN 2000 AND 5000;
    SELECT name, area FROM cities WHERE name IN ('Delhi', 'Shanghai');
    SELECT name, area FROM cities WHERE name NOT IN ('Delhi', 'Shanghai');
    
    -- multiple conditions using AND/OR
    SELECT name, area 
    FROM cities WHERE name IN ('Delhi', 'Shanghai') AND area = 2240;
    
    -- calculation + comparsion operator
    SELECT population / area AS density FROM cities 
    WHERE population / area > 5000;
    
    SELECT population / area AS density FROM cities 
    WHERE density > 5000;  -- ERROR - wrong syntax!
    ```
    

Database design tips:

1. common features have conventional table names and columns 
2. create a separate table for each of you app’s feature
3. state assumptions of the features 
4. features with relationship or ownership should reflect in table design

Relationships:

1. one-to-many relationship → “*has many”*
    
    many-to-one relationship → “*belong to one”* / “*has one”* 
    
    <aside>
    💡 they are the same thing — difference is just of perspective!
    
    school *has many* students (one-to-many) 
    
    students *belongs to one* school (many-to-one)
    
    </aside>
    
2. one-to-one
    
    (Capitol ↔ Country)  
    
3. many-to-many
    
    (student ↔ classes)
    

Keys:

1. Primary key - unique *unmodifiable* identifier of record
    - mostly named `id`
    - either int or uuid
    - postgres has `SERIAL` type which automatically assigns integer by doing +1 (no need to provide id when inserting data)
        
        ```sql
        CREATE TABLe users (
        	id SERIAL PRIMARY KEY,
          username VARCHAR(50)
        );
        ```
        
2. Foreign key - relate a record to another record of another table
    - used to establish relationship between tables
    - in one-to-many, the ‘many’ side of the relationship gets the foreign key column
    - provides data consistency
    - Example: `photos.user_id` refers to `user.id`
        
        ```sql
        CREATE TABLE photos (
        	id SERIAL PRIMARY KEY,
          url VARCHAR(200),
          user_id INTEGER REFERENCES users(id)
        );
        
        INSERT INTO photos (url, user_id) 
        VALUES 
        	('http://25.jpeg', 1),
          ('http://36.jpeg', 1),
        	('http://267.jpeg', 2);
        ```
        
    - join data from both tables