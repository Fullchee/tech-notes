1. A record is "deleted" from a `DELETE`
2. Creates a "dead tuple"
	1. doesn't create empty space yet
3. `VACUUM` removes dead tuples from table and indexes
	1. will not return disk space back to OS
		1. unless you run `VACUUM FULL`
	2. will create space for new rows
4. need to update planning statistics with `ANALYZE`

## `VACUUM FULL`

- gives disk space back to OS
- EXCLUSIVE LOCK on table
	- can't even `SELECT`
- creates a copy of the table
	- doubles the storage needed

## Autovacuum

### Check if autovacuum is on

```sql
SELECT name, setting
FROM pg_settings
WHERE name IN (
  'autovacuum',
  'log_autovacuum_min_duration',
  'autovacuum_max_workers',
  'autovacuum_naptime')
```

```
+-----------------------------+---------+
| name                        | setting |
|-----------------------------+---------|
| autovacuum                  | on      |
| autovacuum_max_workers      | 3       |
| autovacuum_naptime          | 60      |
| log_autovacuum_min_duration | -1      |
+-----------------------------+---------+
```

### Why autovacuum should always be on

1. tons of dead 
2. will run out of transaction IDs
	1. DB will shut down

### View the last time (auto)vacuum was run for a table

```sql
SELECT
  schemaname,
  relname AS table_name,
  last_vacuum,
  last_autovacuum,
  vacuum_count,
  autovacuum_count
FROM pg_stat_user_tables;
```
