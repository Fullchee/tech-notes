
```sql
DROP TABLE IF EXISTS public.my_table;

ALTER TABLE my_table SET SCHEMA public;
```
- easy to change schema of a cache table
- multi-fiscal year calculations are always good
	- always calculates all the things
- performance
	- DROP & SET SCHEMA is very quick
	- doesn’t matter how long it takes to create the table
		- won’t block the database & the app when the actual table is being created


```sql
DELETE FROM public.my_table WHERE fiscal_year = :fiscal_year

INSERT INTO my_table (col1, col2, ...)
  SELECT col1, col2, ...
  FROM my_table
```

drop alter is preferable for the flexibility
