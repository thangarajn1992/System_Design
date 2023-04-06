# Design a store database - Intro

Create your own store! Your store should sell one type of things, like clothing or bikes, whatever you want your store to specialize in. You should have a table for all the items in your store, and at least 5 columns for the kind of data you think you'd need to store. You should sell at least 15 items, and use select statements to order your items by price and show at least one statistic about the items.

```sql
CREATE TABLE bikes(id INTEGER PRIMARY KEY, name TEXT, manufacturer TEXT, year INTEGER, price INTEGER);

INSERT INTO bikes VALUES(1, "Avenger", "Bajaj", 2016, 90000);
INSERT INTO bikes VALUES(2, "Discover", "Bajaj", 2009, 63000);
INSERT INTO bikes VALUES(3, "Activa", "Honda", 2004, 76000);
INSERT INTO bikes VALUES(4, "Unicorn", "Honda", 2006, 82000);
INSERT INTO bikes VALUES(5, "Thunder Bird", "Royal Enfield", 2007, 95000);
INSERT INTO bikes VALUES(6, "Jupiter", "TVS", 2017, 55000);
INSERT INTO bikes VALUES(7, "Ray" , "Yamaka", 2012, 64000);
INSERT INTO bikes VALUES(8, "Fascino", "Yamaka", 2015, 68000);
INSERT INTO bikes VALUES(9, "FZ S", "Yamaka", 2011, 93000);
INSERT INTO bikes VALUES(10, "Scooty Pep", "TVS", 2001, 46000);
INSERT INTO bikes VALUES(11, "XL", "TVS", 1998, 42000);
INSERT INTO bikes VALUES(12, "Gusto", "Mahindra", 2013, 57000);
INSERT INTO bikes VALUES(13, "KTM", "Suzuki", 2014, 95000);
INSERT INTO bikes VALUES(14, "Classic 350", "Royal Enfield", 2008, 123000);
INSERT INTO bikes VALUES(15, "Ntorq 125", "TVS", 2019, 76000);

SELECT year, SUM(price) from bikes GROUP BY year
```

### Query results

| year | SUM(price) |
| ---- | ---------- |
| 1998 | 42000      |
| 2001 | 46000      |
| 2004 | 76000      |
| 2006 | 82000      |
| 2007 | 95000      |
| 2008 | 123000     |
| 2009 | 63000      |
| 2011 | 93000      |
| 2012 | 64000      |
| 2013 | 57000      |
| 2014 | 95000      |
| 2015 | 68000      |
| 2016 | 90000      |
| 2017 | 55000      |
| 2019 | 76000      |
