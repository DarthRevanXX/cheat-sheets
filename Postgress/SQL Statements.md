  
CREATE TABLE cities (

            name VARCHAR(50),

            country VARCHAR(50),

            area INTERGER

);  
  
INSERT INTO cities (

            name, country, population, area

) VALUES (’Tokyo’, ‘Japan’, 387347), (’Tokyo’, ‘Japan’, 387347);  
  
SELECT * FROM cities;  
SELECT name, country FROM cities;

SELECT name, name FROM cities;  
(Can change order, or repeat columns)

Calculated columns(Could do transformation on returning data):  
**Math operators!**  
  
SELECT name, population / area FROM cities;  
rename transformed field:

SELECT name, population / area AS population_density FROM cities;  
  
**String Operators and functions  
  
**|| - join 2 strings  
CONCAT() - JOIN 2 strings  
LOWER() - Gives a lower case string

LENGTH() - Gives number of characters in a string

UPPER() - Gives an upper case string

  
SELECT name || ‘, ’ || country AS location from cities;

SELECT CONCAT(name, ‘, ’, country) AS location from cities;

SELECT CONCAT(UPPER(name), ‘, ’, country) AS location from cities;  
SELECT UPPER(CONCAT(name, ‘, ’, country)) AS location from cities;

**FILTERING RECORDS  
  
**SELECT name, area FROM cities WHERE area > 4000;