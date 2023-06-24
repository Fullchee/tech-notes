# SQL Dates

## Fundamental methods

DATE_TRUNC(''month", date) vs EXTRACT(MONTH from date)

-   `DATE_TRUNC` gets you the date for the first second of the month, year, day, …
    -   `DATE_TRUNC('month', '2022-01-15'::DATE)` -> `2022-01-01 00:00:00-05`
-   `DATE_PART` gets the year/month/date of the date
    -   `DATE_PART('year', '2022-01-15'::DATE)` -> `2022`
    -   `EXTRACT` is the same except it returns numeric instead of float8
-   `CURRENT_DATE` gives the day
    -   example: `2022-01-15
-   `NOW()` also specifies the time

    -   example: `2022-01-14 17:21:13.703974-05`

## Add and subtract dates

- add and subtract dates!
    -   `select '2021-02-01'::DATE - 1` => `2021-01-31'`
Interval


### Filter by date within the current fiscal year (starts Feb 1)

```sql
SELECT *
FROM table
WHERE DATE_PART('year', date_column_name - '1 month'::INTERVAL) =
      DATE_PART('year', CURRENT_DATE::date - '1 month'::INTERVAL)
```


use `BETWEEN` so that you can use the index ????

```sql
SELECT *
FROM table
WHERE col_date BETWEEN 
```

Does >= and < also use the index?

```sql
SELECT *
FROM my_table
WHERE reporting_day >= '2023-02-01'::DATE
  AND reporting_day < '2024-02-01'::DATE
```

### Select the first Friday of the current month

????

#### Day of the week of the 1st

```sql
EXTRACT(DOW FROM DATE_TRUNC('month', CURRENT_DATE))
```

-   gets the DOW of the 1st of the month

DOW of 1st of month -> Day of first Friday
0 -> 6
1 -> 5
2 -> 4
3 -> 3
4 -> 2
5 -> 1
6 -> 7

```sql
CASE
  WHEN (6 - EXTRACT(DOW FROM DATE_TRUNC('month', CURRENT_DATE)) > 0)
    THEN 6 - EXTRACT(DOW FROM DATE_TRUNC('month', CURRENT_DATE)) > 0
  ELSE 7
```

### Group by quarter

```psql
GROUP BY CEIL(month_id / 3)
```


### Date range from string

```sql
'[2022-02-01, 2023-02-01)'::daterange
```


Generate '2022-02-01'::DATE given 2023

```sql
make_date(year int, month int, day int)
```

```sql
SELECT *
FROM 
WHERE UPPER('[2022-02-01, 2023-02-01)'::daterange)c
```


```
SELECT to_char(1, '9th');
```

[Template Patterns & Modifiers for Numeric Formatting in PostgreSQL](https://database.guide/template-patterns-modifiers-for-numeric-formatting-in-postgresql/)