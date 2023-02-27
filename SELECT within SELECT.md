# 4 SELECT within SELECT
1. List each country name where the population is larger than that of 'Russia'. 
```sql
SELECT name
FROM world
WHERE population > (
    SELECT population
    FROM world
    WHERE name='Russia');
```

2. Show the countries in Europe with a per capita GDP greater than 'United Kingdom'. 
```sql
SELECT name
FROM world
WHERE
    gdp/population > (
        SELECT gdp/population
        FROM world
        WHERE name = 'United Kingdom')
    AND continent = 'Europe';
```

3. List the name and continent of countries in the continents containing either Argentina or Australia. Order by name of the country.
```sql
SELECT
    name,
    continent
FROM world
WHERE continent IN (
    SELECT continent
    FROM world
    WHERE name IN ('Argentina', 'Australia'))
ORDER BY name;
```

4. Which country has a population that is more than United Kingom but less than Germany? Show the name and the population.
```sql
SELECT
    name,
    population
FROM world
WHERE
    population > (
        SELECT population
        FROM world
        WHERE name = 'United Kingdom')
    AND population < (
        SELECT population
        FROM world
        WHERE name = 'Germany');
```

5. Show the name and the population of each country in Europe. Show the population as a percentage of the population of Germany.
```sql
SELECT
    name,
    CONCAT(
        ROUND(
            100*population/(
                SELECT population
                FROM world
                WHERE name = 'Germany')), '%') AS percentage
FROM world
WHERE continent = 'Europe';
```

6. Which countries have a GDP greater than every country in Europe? [Give the name only.] (Some countries may have NULL gdp values.)
```sql
SELECT name
FROM world
WHERE gdp > ALL(
    SELECT gdp
    FROM world
    WHERE
        continent = 'Europe' AND
        gdp IS NOT NULL);
```

7. Find the largest country (by area) in each continent, show the continent, the name and the area.
```sql
SELECT
    continent,
    name,
    area
FROM world x
WHERE area >= ALL(
    SELECT area
    FROM world y
    WHERE y.continent=x.continent);
```

8. List each continent and the name of the country that comes first alphabetically.
```sql
SELECT
    continent,
    name
FROM world x
WHERE x.name <= ALL(
    SELECT name
    FROM world y
    WHERE y.continent = x.continent);
```

9. Find the continents where all countries have a population <= 25000000. Then find the names of the countries associated with these continents. Show name, continent and population. 
```sql

```

10. Some countries have populations more than three times that of all of their neighbours (in the same continent). Give the countries and continents.
```sql

```