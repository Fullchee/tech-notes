# SQL Arrays and JSON

## Arrays

```sql
SELECT
ARRAY
  [COL1, COL2]
FROM table
```

![63c31635f1c8fabd69f5224f1a32cc4e.png](63c31635f1c8fabd69f5224f1a32cc4e.png)

### `JSON_BUILD_ARRAY()`

heterogeneous typed JSON array

```sql
> SELECT ARRAY['1', '2', 3, '4']
[1,2,3,4] -- converted to int

> SELECT JSON_BUILD_ARRAY('1', '2', 3, '4')
['1', '2', 3, '4']  -- keeps data types
```

### How UNNEST works

```sql
SELECT
UNNEST(ARRAY\[1,2,3\]) as num1
UNNEST(ARRAY\[4,5\]) as num2
1 as one
```

![4f091a049cccf838fa97c4f8ead2ce88.png](web-dev/backend/database/sql/SQL%20Language/4f091a049cccf838fa97c4f8ead2ce88.png)

### Using UNNEST

```sql
SELECT
UNNEST(ARRAY[
  quota1_building_block_id,
    quota2_building_block_id
    ]) AS rule_block_id,
    *
FROM table_name
```

![0d2b09974a338b8855490ef96c2d6960.png](web-dev/backend/database/sql/SQL%20Language/0d2b09974a338b8855490ef96c2d6960.png)

### ARRAY vs ARRAY_AGG

When there's a `GROUP BY`, aggregate into an array

| id  | forma_id  | accessor_id            |
| --- | --------- | ---------------------- |
| 1   | user's ID | manager's manager's ID |
| 2    |  3         |   4                     |

```sql
WITH data(category, subcategory, amount) AS (
  VALUES ('Quota 1', 'BCR', 123),
         ('Quota 1', 'ICR', 456),
         ('BT', 'BT', 789)
)
SELECT ARRAY_AGG(subcategory)
FROM data
GROUP BY category;

--| array_agg      |
--|----------------|
--| ['BT']         |
--| ['BCR', 'ICR'] |
```

you can also `ARRAY_AGG(table_name)`


#### Turning a table into a JSON array of objects

If I have a table like
```sql
WITH data(category, subcategory, amount) AS (
  VALUES ('Quota 1', 'BCR', 123),
         ('Quota 1', 'ICR', 456),
         ('BT', 'BT', 789)
)
```

```
|category|subcategory|amount|  
+--------+-----------+------+  
|Quota 1 |BCR        |123   |  
|Quota 1 |ICR        |456   |  
|BT      |BT         |789   |
```

and I want the JSON

```json
[
  { "category": "Quota 1", "subcategory": "BCR", "amount": 123 },
  { "category": "Quota 1", "subcategory": "ICR", "amount": 456 },
  { "category": "BT", "subcategory": "BT", "amount": 789 }
]
```

>[!What should the query look like?]-
>```diff
>WITH data(category, subcategory, amount) AS (
>  VALUES ('Quota 1', 'BCR', 123),
>         ('Quota 1', 'ICR', 456),
>         ('BT', 'BT', 789)
>)
>+ SELECT JSON_AGG(data)
>+ FROM data
>```


### JSONB to array

```sql
> TRANSLATE('["ICR"]'::jsonb::text, '[]', '{}')::TEXT[]

{'ICR'}
```

### Index of value in array

If you have an array of objects

```sql
WITH data(category, subcategory, amount) AS (
  VALUES ('Quota 1', 'BCR', 123),
         ('Quota 1', 'ICR', 456),
         ('BT', 'BT', 789)
)
SELECT JSON_AGG(result)
FROM data
select * FROM json_array
```

```json
[
	{"name": "BCR", "value": 123},
	{"name": "ICR", "value": 456},
	{"name": "ACR", "value": 789}
]
```

[!Get the ICR value]-




```sql
ARRAY_POSITION('{"ICR", "ACR"}'::TEXT[], 'ICR')
```

## JSON

### [JSON vs JSONB in Postgres](https://stackoverflow.com/a/39637548/8479344](https://stackoverflow.com/a/39637548/8479344)

-   `jsonb`
    -   mostly use this
    -   has an actual data structure, has actual operations, concatenation, …
-   `json` stores it as plain text with whitespace
    -   can't do those operations
    -   use if you're processing logs and use it more like an audit trail

### [-> vs ->>](https://www.postgresqltutorial.com/postgresql-json/)

-   `->` returns the result as JSON
    -   great to get nested objects
-   `->>` returns the result as text

Column name: info

```json
{
    "customer": "Lily Bush",
    "items": {
        "product": "Diaper",
        "qty": 24
    }
}
```

```sql
SELECT info -> 'items' ->> 'product'
-- Diaper as text
```

### JSON_AGG

like ARRAY_AGG, 

```sql
WITH my_table(str_key, int_key, null_key) AS (
  VALUES ('commission', 123, NULL),
         ('adjustment', 456, NULL),
         ('spiff', 789, NULL)
)
SELECT json_agg(my_table) AS col_name FROM my_table;

--+-----------------------------------------------------------+
--| col_name                                                  |
--|-----------------------------------------------------------|
--| [{"str_key":"commission","int_key":123,"null_key":null},  |
--|  {"str_key":"adjustment","int_key":456,"null_key":null},  |
--|  {"str_key":"spiff","int_key":789,"null_key":null}]       |
--+-----------------------------------------------------------+
```

### JSONB_OBJECT

-   Takes in two string arrays (they must be strings) of keys and values and zips them together
-   need more than just strings?
    -   Use `json_build_object(key1, value1, key2, value2, ...)`
- 

```sql
WITH data(category, subcategory, amount) AS (
  VALUES ('Quota 1', 'BCR', 123),
         ('Quota 1', 'ICR', 456),
         ('BT', 'BT', 789)
)
SELECT
  category,
  ARRAY_AGG(subcategory),
  ARRAY_AGG((amount)::TEXT),
  JSONB_OBJECT(ARRAY_AGG(subcategory), ARRAY_AGG((amount)::TEXT)) AS breakdown
FROM data
GROUP BY category
ORDER BY ARRAY_POSITION(ARRAY['Quota 1', 'Quota 2', 'BT', 'KSO'], category)
```

![Image not found: ../0cbb118e22f89e2847dce5a70400860c.png](0cbb118e22f89e2847dce5a70400860c.png)

### JSON to String

```sql
SELECT jsoncol #>> '{}'
FROM mytable;
```

????


## Ordinality

Adds a new `bigint` column
- starts with 1

Retain the original position of each element

Useful in aggregations

[Ordinality video](https://fullchee-reminders.netlify.app/link/2183)


```sql
SELECT * FROM UNNEST(string_to_array('here is a string', ' '))
```

```
+--------+
| unnest |
|--------|
| here   |
| is     |
| a      |
| string |
+--------+
```

### Simple example of using ORDINALITY

```sql
SELECT * FROM UNNEST(string_to_array('here is a string', ' '))
WITH ORDINALITY AS table_name(word, item_position)
```

```
+--------+------------+
| word   | item_position |
|--------+------------|
| here   | 1          |
| is     | 2          |
| a      | 3          |
| string | 4          |
+--------+------------+
```

```sql
SELECT * FROM UNNEST(string_to_array('here is a string', ' '))
WITH ORDINALITY AS table_name(word, item_position)
ORDER BY table_name.item_position DESC
```

```
+--------+------------+
| word   | item_position |
|--------+------------|
| string | 4          |
| a      | 3          |
| is     | 2          |
| here   | 1          |
+--------+------------+
```


### Real life example of using Ordinality

```sql
SELECT UNNEST(ARRAY[1,2,3,4,5]);
UNION ALL
SELECT UNNEST(ARRAY[-1, -2, -3, -4, -5])
```