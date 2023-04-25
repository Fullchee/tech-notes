# SQL Ranges

[[sql-dates]]

## Multiranges

[Multiranges in PostgreSQL 14](https://www.cybertec-postgresql.com/en/multiranges-in-postgresql-14/)

```sql
test=# SELECT int4multirange(
int4range(10, 20),
int4range(12, 25),
int4range(38, 42)
);
int4multirange
-------------------
{[10,25),[38,42)}
(1 row)
```

overlapping ranges?

-   it’ll resolve into a non-overlapping set 🤯


## Range Operators

`<@`
- range/element is contained by

```sql
SELECT int4range(3,5) <@ int4range(2,8);  -- t
```



`@>`
- contains range, element

```sql
SELECT int4range(3,5) @> int4range(3,4);  -- t
```

```sql
SELECT '[2014-01-01,2014-04-01)'::tsrange @> '2014-03-10'::timestamp;  -- t
```


### Overlaps operator `&&`


```sql
SELECT *
FROM
  (VALUES
    ('[2021-06-01,2022-01-01)'::DATERANGE),
    ('[2021-02-01,2021-06-07)'::DATERANGE),
    ('[2020-02-01,2022-02-01)'::DATERANGE),
    ('[2021-12-01,2022-02-01)'::DATERANGE),
    -- doesn't overlap
    ('[2025-01-01,2026-02-01)'::DATERANGE)
  )
AS column_names(range)

WHERE range && '[2021-01-01, 2022-01-01)'::daterange
```

