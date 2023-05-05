

## Temp table
```sql
CREATE TEMPORARY TABLE temp_table_name (
  col1 INT,
  col2 INT
)
```

- can only access in the current session

>[!Physical table vs temp table (thread performance)]-
>temp tables: need sequences and workarounds when using several workers
>cause you can't create the same table twice???


[performance - PostgreSQL temporary tables - Stack Overflow](https://stackoverflow.com/a/555655/8479344)

## Unlogged table

```sql
CREATE UNLOGGED TABLE my_table (
  col1 INT,
  col2 INT
)
```



>[!Unlogged table vs temp table for performance]-
>- [both equally fast](https://stackoverflow.com/a/64696612/8479344)
>	- both bypass WAL
>		- write-ahead logging
>- only diff: buffer (cache) sizetemp tables are cached in process private memory
>	- temp table
>		- `temp_buffers` param sets limit for process private memory
>	- unlogged table
>		- shared_buffers


>[!Downside of unlogged table]-
>not ACID compliant
>- if the DB crashes, can't recover


## What is a CTE?
- common table expression
- does it store it in memory?

>[!CTE vs temporary view/table]-
>- scope
>- CTE is only available for the query
>- temp table/view is available for all queries in the current session

[sql server - Which are more performant, CTE or temporary tables? - Stack Overflow](https://stackoverflow.com/questions/690465/which-are-more-performant-cte-or-temporary-tables)

## Materialized view

## Materialized CTE

[postgresql - Are there side effects to Postgres 12's NOT MATERIALIZED directive? - Database Administrators Stack Exchange](https://dba.stackexchange.com/questions/257014/are-there-side-effects-to-postgres-12s-not-materialized-directive)

?


## When to use each?

it depends 

- read the EXPLAIN analyze
- run experiments
