# MySQL 8.0 = SQL + NoSQL
MySQL has two ports: classic protocol (3306) and X protocol (33060). X protocol is used for SQL + NoSQL. </br>
Connect to database using Port **33060** with JavaScript (JS) on MySQL Shell
```
mysqlsh root@localhost:33060
```
On MySQL Shell, query JSON document **countryinfo** under database world_x (NoSQL)
```
session.getSchema('world_x').getCollection('countryinfo').find();
```
Query only the 1st 2 records from countryinfo
```
session.getSchema('world_x').getCollection('countryinfo').find().limit(2);
```
Using variable to query data
```
colCI = session.getSchema('world_x').getCollection('countryinfo');
colCI.find().limit(2);
```
Query countryinfo only for NAME like 'J%' and show only the first 2 records
```
colCI.find("Name LIKE 'J%'").limit(2);
```
Do you like to use Python ? </br>
MySQL Shell supports Python as well. We can do the same query using Python
```
\py
session.get_schema('world_x').get_collection('countryinfo').find()
session.get_schema('world_x').get_collection('countryinfo').find().limit(2)
colCI = session.get_schema('world_x').get_collection('countryinfo');
colCI.find().limit(2);
colCI.find("Name LIKE 'J%'").limit(2);
```
Do you like to use SQL ? </br>
Definitely MySQL is an SQL database, so you can use SQL. </br>
Switch to use SQL and formatting JSON document in SQL as follow:
```
\sql
use world_x;
SELECT doc->>'$.Name' AS Name, doc->>'$.demographics.Population' AS Population, doc->>'$.geography.SurfaceArea' AS SurfaceArea FROM countryinfo WHERE doc->>'$.Name' LIKE "J%" AND doc->>'$.geography.Continent' = 'Asia';
```
Using SQL but output in JSON:
```
SELECT JSON_OBJECT("Name", doc->>'$.Name', "Population", doc->>'$.demographics.Population', "SurfaceArea", doc->>'$.geography.SurfaceArea') AS results FROM countryinfo WHERE doc->>'$.Name' LIKE "J%" AND doc->>'$.geography.Continent' = 'Asia';
```
Combining SQL tables and NoSQL JSON Documment using SQL statement:
```
SELECT
	JSON_OBJECT(
	"Country", country.Name,
        "Capital", city.Name,
        "Percent", round(city.Info->>'$.Population'/countryinfo.doc->>'$.demographics.Population'*100, 2)
        ) AS Results
FROM
	countryinfo, city, country
WHERE
	country.Name LIKE "J%"
	AND
	countryinfo.doc->>'$.geography.Continent' = 'Asia'
    AND
	countryinfo.doc->>'$.Name'= country.Name
	AND
	country.Capital = city.ID
  ```
