

## Hardcoded table

```sql
CREATE TABLE table_name(name1, name2) AS (
  VALUES ('value1', FALSE),
         ('value2', TRUE)
)
```

```sql
-- | name1  | name2 | arr_col    |
-- |--------+-------+------------|
-- | value1 | False | [123, 456] |
-- | value2 | True  | [789]      |
WITH cte_name (name1, name2, hardcoded_array, hardcoded_json) AS (
  VALUES ('value1', FALSE, ARRAY [123,456], '{}':JSON)
)
SELECT *
FROM cte_name
```

### Hardcoded table in a FROM

```sql
SELECT *
FROM
  (VALUES
    ('Col1 Item 1', 'Col2 Item 1', 'Col3 Item 1', NULL),
    ('Col1 Item 2', 'Col2 Item 2', 'Col3 Item 2', FALSE)
  )
AS my_table_name(col1, col2, col3, bool_col)
```


## `generate_series`

### In a `SELECT`

```sql
SELECT GENERATE_SERIES(1,5) AS my_col;
```


```
+--------+
| my_col |
|--------|
| 1      |
| 2      |
| 3      |
| 4      |
| 5      |
+--------+
```

### `generate_series` in a `FROM`

```sql
SELECT i
FROM GENERATE_SERIES(1,5) AS s(i);
```

```
+--+  
|i |  
+--+  
|1 |  
|2 |  
|3 |  
|4 |
|5 |
+--+
```

### Series of months

```sql
SELECT
  GENERATE_SERIES(
    '2023-02-01'::DATE,
    '2024-01-31'::DATE,
    INTERVAL '1 MONTH'
  )::DATE AS month
```

```
+------------+
| month      |
|------------|
| 2023-02-01 |
| 2023-03-01 |
| 2023-04-01 |
| 2023-05-01 |
| 2023-06-01 |
| 2023-07-01 |
| 2023-08-01 |
| 2023-09-01 |
| 2023-10-01 |
| 2023-11-01 |
| 2023-12-01 |
| 2024-01-01 |
+------------+
```

```sql
SELECT "month"
  FROM GENERATE_SERIES(
      ( 2023 || '-02-01')::DATE,
      ( 2023 ::INT + 1 || '-01-31')::DATE,
      INTERVAL '1 MONTH'
    ) AS "month"
```
