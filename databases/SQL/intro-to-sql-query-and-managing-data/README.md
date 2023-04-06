# Intro to SQL: Query and Managing Data

### Command List Used in this course

```sql
CREATE TABLE groceries (id INTEGER PRIMARY KEY, name TEXT, quantity INTEGER, aisle INTEGER);
INSERT INTO groceries VALUES (1, "Bananas", 4, 7);
SELECT name FROM groceries
SELECT * FROM groceries
SELECT * FROM groceries ORDER BY aisle
SELECT * FROM groceries WHERE aisle > 5 ORDER BY aisle;
SELECT SUM(quantity) FROM groceries;
SELECT aisle, SUM(quantity) FROM groceries GROUP BY aisle;

SELECT * FROM exercise_logs WHERE calories > 50 ORDER BY calories;
SELECT * FROM exercise_logs WHERE calories > 50 AND minutes < 30;
SELECT * FROM exercise_logs WHERE calories > 50 OR heart_rate > 100;

SELECT * FROM exercise_logs WHERE type = "biking" OR type = "hiking" OR type = "tree climbing" OR type = "rowing";
SELECT * FROM exercise_logs WHERE type IN ("biking", "hiking", "tree climbing", "rowing");
SELECT * FROM exercise_logs WHERE type NOT IN ("biking", "hiking", "tree climbing", "rowing");

SELECT * FROM exercise_logs WHERE type IN (SELECT type FROM drs_favorites);
SELECT * FROM exercise_logs WHERE type IN (
    SELECT type FROM drs_favorites WHERE reason LIKE "%cardiovascular%");
```

1. [Introduction to SQL](introduction-to-sql.md)
2. [More Advanced SQL Queries](more-advanced-sql-queries.md)
