# 2 SELECT from World
1. Observe the result of running this SQL command to show the name, continent and population of all countries.
```sql
SELECT
    name,
    continent,
    population
FROM world;
```

2. Show the name for the countries that have a population of at least 200 million.
200 million = 200000000
```sql
SELECT name
FROM world
WHERE population >= 200000000;
```

3. Give the name and the **per capita GDP** for those countries with a population of at least 200 million.
per capita GDP = GDP / population
```sql
SELECT
    name,
    gdp/population
FROM world
WHERE population >= 200000000;
```

4. Show the name and population in millions for the countries of the continent 'South America'. Divide the population by 1000000 to get population in millions. 
```sql
SELECT
    name,
    population/1000000 AS population
FROM world
WHERE continent = 'South America';
```

5. Show the name and population for France, Germany, Italy.
```sql
SELECT
    name,
    population
FROM world
WHERE name IN ('France', 'Germany', 'Italy');
```

6. Show the countries which have a name that includes the word 'United'.
```sql
SELECT name
FROM world
WHERE name LIKE '%United%';
```

7. Two ways to be big: A country is **big** if it has an area of more than 3 million sq km or it has a population of more than 250 million.

Show the countries that are big by area or big by population. Show name, population and area.
```sql
SELECT
    name,
    population,
    area
FROM world
WHERE area > 3000000 OR population >= 250000000;
```

8. Show the countries that are big by area (more than 3 million) or big by population (more than 250 million) **but not both**. Show name, population and area.
```sql
SELECT
    name,
    population,
    area
FROM world
WHERE (area > 3000000 AND population < 250000000) OR (population >= 250000000 AND area <= 3000000);
```

9. Show the name and population in millions and the GDP in billions for the countries of the continent 'South America'. Use the ROUND function to show the values to two decimal places.
```sql
SELECT
    name,
    ROUND(population/1000000, 2) AS population,
    ROUND(gdp/1000000000, 2) AS gdp
FROM world
WHERE continent = 'South America';
```

10. Show per-capita GDP for the trillion dollar countries to the nearest $1000.
```sql
SELECT
    name,
    ROUND(gdp/population, -3) AS gdp
FROM world
WHERE gdp >= 1000000000000;
```

11. Show the name and capital where the name and the capital have the same number of characters.
```sql
SELECT
    name,
    capital
FROM world
WHERE LENGTH(name) = LENGTH(capital);
```

12. Show the name and the capital where the first letters of each match. Don't include countries where the name and the capital are the same word.
```sql
SELECT
    name,
    capital
FROM world
WHERE LEFT(name, 1) = LEFT(capital, 1) AND name <> capital;
```

13. Find the country that has all the vowels and no spaces in its name.
```sql
SELECT name
FROM world
WHERE name LIKE '%a%'
    AND name LIKE '%e%'
    AND name LIKE '%i%'
    AND name LIKE '%o%'
    AND name LIKE '%u%'
    AND name NOT LIKE '% %';
```