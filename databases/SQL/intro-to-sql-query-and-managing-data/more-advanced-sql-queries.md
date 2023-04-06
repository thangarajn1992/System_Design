# More Advanced SQL Queries

### More Complex Queries with AND/OR

```sql
CREATE TABLE exercise_logs
    (id INTEGER PRIMARY KEY AUTOINCREMENT,
    type TEXT,
    minutes INTEGER, 
    calories INTEGER,
    heart_rate INTEGER);


INSERT INTO exercise_logs(type, minutes, calories, heart_rate) VALUES ("biking", 30, 100, 110);
INSERT INTO exercise_logs(type, minutes, calories, heart_rate) VALUES ("biking", 10, 30, 105);
INSERT INTO exercise_logs(type, minutes, calories, heart_rate) VALUES ("dancing", 15, 200, 120);

SELECT * FROM exercise_logs;
```

#### Query results

| id | type    | minutes | calories | heart\_rate |
| -- | ------- | ------- | -------- | ----------- |
| 1  | biking  | 30      | 100      | 110         |
| 2  | biking  | 10      | 30       | 105         |
| 3  | dancing | 15      | 200      | 120         |

1. **AUTOINCREMENT** -> It means that database will automatically increment and fill it for us as we add new entries.
2. While inserting data into tables, we have different syntax here where we specify the column names before the actual values. This way we can insert data into only specific columns instead of all the columns in our database.

```sql
// Query to find the activities where we burned more than 50 calories
// and sort it by the calories burnt

SELECT * FROM exercise_logs WHERE calories > 50 ORDER BY calories;


Query results
id 	type 	minutes 	calories 	heart_rate
1 	biking 	30 	100 	110
3 	dancing 	15 	200 	120
```

#### AND

```sql
// Query to find the activites where we burned more than 50 calories
// and also time spent being less than 30 mins

SELECT * FROM exercise_logs WHERE calories > 50 AND minutes < 30;

Query results
id 	type 	minutes 	calories 	heart_rate
3 	dancing 	15 	200 	120
```

#### OR

```sql
//Query to find most rigourous exercise where we burned more than 50 calories
// or our heart rate is above 100

SELECT * FROM exercise_logs WHERE calories > 50 OR heart_rate > 100;

Query results
id 	type 	minutes 	calories 	heart_rate
1 	biking 	30 	100 	110
2 	biking 	10 	30 	105
3 	dancing 	15 	200 	120
```

AND has more precedence than OR in general. We can use parenthesis to change the precedence.

### Querying IN subqueries

```sql
CREATE TABLE exercise_logs
    (id INTEGER PRIMARY KEY AUTOINCREMENT,
    type TEXT,
    minutes INTEGER, 
    calories INTEGER,
    heart_rate INTEGER);

INSERT INTO exercise_logs(type, minutes, calories, heart_rate) VALUES ("biking", 30, 100, 110);
INSERT INTO exercise_logs(type, minutes, calories, heart_rate) VALUES ("biking", 10, 30, 105);
INSERT INTO exercise_logs(type, minutes, calories, heart_rate) VALUES ("dancing", 15, 200, 120);
INSERT INTO exercise_logs(type, minutes, calories, heart_rate) VALUES ("tree climbing", 30, 70, 90);
INSERT INTO exercise_logs(type, minutes, calories, heart_rate) VALUES ("tree climbing", 25, 72, 80);
INSERT INTO exercise_logs(type, minutes, calories, heart_rate) VALUES ("rowing", 30, 70, 90);
INSERT INTO exercise_logs(type, minutes, calories, heart_rate) VALUES ("hiking", 60, 80, 85);
```

#### Query results

| id | type          | minutes | calories | heart\_rate |
| -- | ------------- | ------- | -------- | ----------- |
| 1  | biking        | 30      | 100      | 110         |
| 2  | biking        | 10      | 30       | 105         |
| 3  | dancing       | 15      | 200      | 120         |
| 4  | tree climbing | 30      | 70       | 90          |
| 5  | tree climbing | 25      | 72       | 80          |
| 6  | rowing        | 30      | 70       | 90          |
| 7  | hiking        | 60      | 80       | 85          |

```sql
//Query to find all outdoor activities
SELECT * FROM exercise_logs WHERE type = "biking" OR type = "hiking" OR type = "tree climbing" OR type = "rowing";

Query results
id 	type 	minutes 	calories 	heart_rate
1 	biking 	30 	100 	110
2 	biking 	10 	30 	105
4 	tree climbing 	30 	70 	90
5 	tree climbing 	25 	72 	80
6 	rowing 	30 	70 	90
7 	hiking 	60 	80 	85

// Same query becomes more easy with "IN" 

/* IN */
SELECT * FROM exercise_logs WHERE type IN ("biking", "hiking", "tree climbing", "rowing");
Query results
id 	type 	minutes 	calories 	heart_rate
1 	biking 	30 	100 	110
2 	biking 	10 	30 	105
4 	tree climbing 	30 	70 	90
5 	tree climbing 	25 	72 	80
6 	rowing 	30 	70 	90
7 	hiking 	60 	80 	85

// Query to get indoor using NOT operator

SELECT * FROM exercise_logs WHERE type NOT IN ("biking", "hiking", "tree climbing", "rowing");
Query results
id 	type 	minutes 	calories 	heart_rate
3 	dancing 	15 	200 	120

```

Now we are adding another table as activities recommended by doctors

```sql
CREATE TABLE drs_favorites
    (id INTEGER PRIMARY KEY,
    type TEXT,
    reason TEXT);

INSERT INTO drs_favorites(type, reason) VALUES ("biking", "Improves endurance and flexibility.");
INSERT INTO drs_favorites(type, reason) VALUES ("hiking", "Increases cardiovascular health.");
```

Using IN operator, we can make use of result of another query. i.e One query's result can be fed as condition for IN operator as below:

```sql
//Query to find activity that are recommended by doctors
SELECT * FROM exercise_logs WHERE type IN (SELECT type FROM drs_favorites);
Query results
id 	type 	minutes 	calories 	heart_rate
1 	biking 	30 	100 	110
2 	biking 	10 	30 	105
7 	hiking 	60 	80 	85

// Query to find activity that doctor recommended for cardio-vascular reasons
SELECT * FROM exercise_logs WHERE type IN (
    SELECT type FROM drs_favorites WHERE reason = "Increases cardiovascular health.");
    
// In the above query, we tried to do exact match. 
// But we can improve it by doing in-exact match using LIKE operator.

SELECT * FROM exercise_logs WHERE type IN (
    SELECT type FROM drs_favorites WHERE reason LIKE "%cardiovascular%");

// This will match any entry with reason that has cardiovascular in it.
Query results
id 	type 	minutes 	calories 	heart_rate
7 	hiking 	60 	80 	85
```

### Restricting Grouped Results with HAVING

