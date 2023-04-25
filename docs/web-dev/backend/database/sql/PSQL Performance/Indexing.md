Faster reads and queries 

>[!Why is it important to have fast reads? ]-
>Slow queries are usually the first performance bottleneck in an app


### [[PSQL Query Optimization]]


## Creating

```sql
DROP INDEX IF EXISTS table_column_index;
CREATE INDEX IF NOT EXISTS table_column_index
   ON table (column_name);
```


Index name: max 63 chars


## Reindex vs dropping and creating

`REINDEX` locks writes, but not reads.

`DROP INDEX` locks writes and reads, then `CREATE INDEX` locks writes only.

1. `CREATE INDEX CONCURRENTLY`
2. DROP old index
3. rename new index as the original name

* Longer build time
* minimum lock time

## Rename an index

```sql
ALTER INDEX [IF EXISTS] name_of_index
  RENAME TO new_indexname;
```