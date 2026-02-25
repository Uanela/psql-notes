# 2 Chapter - The SQL Language

## 2.1 Intro

```bash
psql -s mydb
\i basics.sql
```

- `\i` -> reads in commands from specified file
- `-s` -> puts you in single step mode which pauses before sending each statement to the server

## 2.2 Concepts

- PostgreSQL is a `RDBMS`
- relation is mathematical term of table.

## 2.3 Creating a New Table

```sql
CREATE TABLE weather (
    city VARCHAR(80),
    temp_lo INT, -- low temperature
    temp_hi INT, -- high temperature
    prcp REAL, -- precipitation
    date DATE
);

CREATE TABLE cities (
    name VARCHAR(80),
    location POINT
);

DROP TABLE tablename;
```

### 2.4 Populating a Table With Rows

```sql
INSERT INTO weather VALUES ('Beira', 46, 50, 0.25, '1994-11-27')
INSERT INTO cities VALUES ('Beira', '(-194.0, 53.0)')

-- With name fields
INSERT INTO weather (city, temp_lo, temp_hi, prcp, date) VALUES ('Beira', 46, 50, 0.25, '1994-11-27')
INSERT INTO cities VALUES ('Beira', '(-194.0, 53.0)')
```

```bash
COPY weather FROM '/home/user/weather.txt' -- You can use instead \copy from psql
```

### 2.5 Querying a Table

```sql
SELECT * FROM weather;
SELECT city, temp_lo, temp_hi, prcp date FROM weather;
SELECT city, (temp_hi+temp_lo)/2 AS temp_avg, date FROM weather;

SELECT * FROM weather WHERE city = 'Beira' AND prcp > 0.0;
SELECT * FROM weather ORDER BY city;
SELECT DISTINCT city FROM weather ORDER BY city;
```

## 2.6 Joins Between Tables

### Inner Joins

The table on the left side of `JOIN` won't also appear if there aren't matches with the joining table.

- You can write `INNER JOIN` or simply `JOIN`

```sql
SELECT * FROM weather JOIN cities ON city = name;
SELECT city, temp_lo, temp_hi, prcp FROM weather JOIN cities ON city = name;

SELECT weather.city, weather.temp_lo, weather.temp_hi, weather.prcp, cities.location FROM weather JOIN cities ON weather.wity = cities.name;

SELECT * FROM weather, cities WHERE city = name;
```

### Outer Joins

Differently here, the left side of `JOIN` will appear whether there are matches or not if using `LEFT JOIN` if `RIGHT JOIN` the contrary will happen. whereas for `FULL JOIN` it fills with `null` both side of the join and only works for `merge-joinable` and `hash-joinable` join conditions

- you can write `<SIDE> OUTER JOIN` or simply `<SIDE> JOIN`

### Labeling

This code does what you think it does.

```sql
SELECT w1.*, w2.* FROM weather w1 JOIN weather w2 ON w1.temp_lo < w2.temp_lo AND w1.temp_hi > w2.temp_hi;

SELECT * FROM weather w JOIN cities c ON w.city = c.name;
```

## 2.7 Aggregate Functions

- Common aggregate functions: `count()`, `sum()`, `avg()`, `max()` and `min()`

```ts
SELECT MAX(temp_lo) FROM weather;

-- Group By
SELECT city, MAX(temp_lo) FROM weather GROUP BY city;

-- Nested
SELECT city FROM weather FROM where temp_lo = (SELECT MAX(temp_lo) FROM weather);

-- Group By + Having
SELECT city, count(*), max(temp_lo) max_temp_lo FROM weather GROUP BY city HAVING max(temp_lo) < 25;
```

- `HAVING` deals with values after being aggregated whereas `WHERE` decides what will be on the aggregated values to be used in `HAVING`

```sql
-- Getting cities where name starts with `S`
SELECT city, count(*), max(temp_lo) FROM weather WHERE city LIKE 'S%' GROUP BY city;

SELECT city, count(*) FILTER (WHERE temp_lo < 45), max(temp_lo) FROM weather GROUP BY city;
```

- `FILTER` -> behaves like `WHERE`, except it removes rows only from the input of the particular aggregate function that it is attached to.

## 2.8 Updates

```sql
UPDATE weather SET temp = temp_hi - 2, temp_lo - 2 WHERE date > '2002-11-28';
```

- BE CAUTIONS WITH UPDATES WITOUT `WHERE` CLAUSE

## 2.9 Deletions

```sql
DELETE FROM weather WHERE city = 'Hayward';
```

- BE CAUTIONS WITH DELETES WITOUT `WHERE` CLAUSE
