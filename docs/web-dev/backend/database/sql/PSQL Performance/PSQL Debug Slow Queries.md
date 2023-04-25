[Useful PostgreSQL Queries and Commands · GitHub](https://gist.github.com/rgreenjr/3637525)

AWS RDS ran out of IOPS burst balance
Very inefficient queries were thrashing
Had to update the query and kill the currently running queries

The queries weren't holding locks, just trying to join massive tables

[Exploring Query Locks in Postgres - Big elephants](http://big-elephants.com/2013-09/exploring-query-locks-in-postgres/)

## Resources with locks

MVCC: Multi Version Concurrency Control
- [PostgreSQL: Documentation: 9.3: Concurrency Control](https://www.postgresql.org/docs/9.3/mvcc.html)

`pg_locks` table
- locks held by open transactions

[`pg_class`](https://www.postgresql.org/docs/current/catalog-pg-class.html)
- catalog of tables, indexes, sequences, views, composite types, TOAST

[`pg_stat_activity`](https://www.postgresql.org/docs/current/monitoring-stats.html#MONITORING-PG-STAT-ACTIVITY-VIEW)
- all server processes
	- query: the last query the process ran
	- `pid`: process ID
```sql title="find_locks.sql"
-- find_locks.sql
SELECT mode, *
FROM pg_locks l
  JOIN pg_class t ON l.relation = t.oid AND t.relkind = 'r';
```

```sql title="blocking_pids.sql"
-- blocking_pids.sql
-- https://stackoverflow.com/questions/26489244/how-to-detect-query-which-holds-the-lock-in-postgres
SELECT pid, 
       usename, 
       pg_blocking_pids(pid) as blocked_by, 
       query as blocked_query
FROM pg_stat_activity
WHERE cardinality(pg_blocking_pids(pid)) > 0;
```

[Lock Monitoring - PostgreSQL wiki](https://wiki.postgresql.org/wiki/Lock_Monitoring)

```sql
  SELECT blocked_locks.pid     AS blocked_pid,
         blocked_activity.usename  AS blocked_user,
         blocking_locks.pid     AS blocking_pid,
         blocking_activity.usename AS blocking_user,
         blocked_activity.query    AS blocked_statement,
         blocking_activity.query   AS current_statement_in_blocking_process
   FROM  pg_catalog.pg_locks         blocked_locks
    JOIN pg_catalog.pg_stat_activity blocked_activity  ON blocked_activity.pid = blocked_locks.pid
    JOIN pg_catalog.pg_locks         blocking_locks 
        ON blocking_locks.locktype = blocked_locks.locktype
        AND blocking_locks.database IS NOT DISTINCT FROM blocked_locks.database
        AND blocking_locks.relation IS NOT DISTINCT FROM blocked_locks.relation
        AND blocking_locks.page IS NOT DISTINCT FROM blocked_locks.page
        AND blocking_locks.tuple IS NOT DISTINCT FROM blocked_locks.tuple
        AND blocking_locks.virtualxid IS NOT DISTINCT FROM blocked_locks.virtualxid
        AND blocking_locks.transactionid IS NOT DISTINCT FROM blocked_locks.transactionid
        AND blocking_locks.classid IS NOT DISTINCT FROM blocked_locks.classid
        AND blocking_locks.objid IS NOT DISTINCT FROM blocked_locks.objid
        AND blocking_locks.objsubid IS NOT DISTINCT FROM blocked_locks.objsubid
        AND blocking_locks.pid != blocked_locks.pid

    JOIN pg_catalog.pg_stat_activity blocking_activity ON blocking_activity.pid = blocking_locks.pid
   WHERE NOT blocked_locks.granted;
```


## Long running PSQL queries

[Finding and killing long running queries on PostgreSQL](https://medium.com/little-programming-joys/finding-and-killing-long-running-queries-on-postgres-7c4f0449e86d)

```sql TI:"kill_long_running_pids.sql"
WITH long_running_queries AS (
SELECT
  pid,
  now() - pg_stat_activity.query_start AS duration,
  query,
  state
FROM pg_stat_activity
WHERE (now() - pg_stat_activity.query_start) > interval '2 minutes'
  AND state = 'active'
)
SELECT pg_cancel_backend(pid)
FROM long_running_queries
```

Result

```
| pid   | duration               | query       | state  |
| 14183 | 1:52:02.686858         | COMMIT      | idle   |
| 24731 | 5 days, 4:01:05.452130 | COMMIT      | idle   |
| 12640 | 4 days, 1:46:53.366550 | COMMIT      | idle   |
| 19825 | 4:53:19.809795         | SELECT * ...| active |
```


## Kill a process

```sql
SELECT pg_cancel_backend(__pid__);
```

If that doesn't work

```sql
SELECT pg_terminate_backend(__pid__);
```

- may lead to full database restart

## Find large queries

```sql
SELECT nspname || '.' || relname AS "relation",
  pg_size_pretty(pg_total_relation_size(C.oid)) AS "total_size"
FROM pg_class C
LEFT JOIN pg_namespace N ON (N.oid = C.relnamespace)
WHERE nspname NOT IN ('pg_catalog', 'information_schema')
  AND C.relkind <> 'i'
  AND nspname !~ '^pg_toast'
ORDER BY pg_total_relation_size(C.oid) DESC
LIMIT 10;
```

```sql
-- queries that are currently running
SELECT pid, age(clock_timestamp(), query_start), usename, query
FROM pg_stat_activity
WHERE query != '<IDLE>'
  AND query NOT ILIKE '%pg_stat_activity%'
  AND query NOT IN ('', chr(10), 'COMMIT')
ORDER BY query_start desc;
```


```sql title="find_duplicate_tuples.sql"
SELECT (table_name.*)::text, count(*)
FROM table_name
GROUP BY table_name.*
HAVING count(*) > 1;
```


```sql
SELECT
  pid,
  now() - pg_stat_activity.query_start AS duration,
  query,
  state
FROM pg_stat_activity
WHERE pid = 17081;
order by duration desc
```

17081
13484
17656