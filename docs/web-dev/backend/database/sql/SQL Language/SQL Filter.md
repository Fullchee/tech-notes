Standard ANSI SQL

- partially aggregate data
- `WHERE` clause for aggregate data****
	- vs `HAVING`

```sql
SELECT
    COUNT(*) AS unfiltered,
    COUNT(*) FILTER (WHERE i < 5) AS sub_five,
    AVG(i) FILTER (WHERE i < 5) AS avg_sub_five,
    AVG(CASE
        WHEN i < 5 THEN 0
        WHEN i >= 5 THEN 1
        ELSE NULL -- implicit ELSE
        END) AS sub_five_case
FROM GENERATE_SERIES(1,10) AS s(i);
```

```
|unfiltered|sub_five|avg_sub_five|sub_five_case|  
+----------+--------+------------+-------------+  
```

> [!Query result]-
> ```
> |unfiltered|sub_five|avg_sub_five|sub_five_case|  
> +----------+--------+------------+-------------+  
> |10        |5      |2.5         |0.6          |
> ```


## Filter vs Group By and Having

```sql
WITH sales(rep_id, territory, earnings) AS (
  VALUES (1, 'A', 10),
         (1, 'B', 20),
         (2, 'C', 30),
         (2, 'D', 40),
         (3, 'B', 100),
         (4, 'B', 0)  -- gets filtered out by the HAVING
)
SELECT
    rep_id,
    SUM(earnings) AS earnings,
    SUM(earnings) FILTER (WHERE territory != 'B') AS earnings_without_b,
    SUM(earnings) FILTER (WHERE territory != 'D') AS earnings_without_d
FROM sales
GROUP BY rep_id
HAVING SUM(earnings) > 0;
```

```
|rep_id|earnings|earnings_without_b|earnings_without_d|  
```

> [!Query with FILTER and GROUP BY result]-
> ```
> +------+--------+------------------+------------------+  
> |rep_id|earnings|earnings_without_b|earnings_without_d|  
> +------+--------+------------------+------------------+  
> |1     |30      |10                |30                |  
> |3     |100     |NULL              |100               |  
> |2     |70      |70                |30                |  
> +------+--------+------------------+------------------+
> ```

- `GROUP BY` and `HAVING` apply first
- then `FILTER`  takes effect after
- you don't need `GROUP BY` to use `FILTER`
	- `FILTER` does an aggregation on a filtered subset of the queries