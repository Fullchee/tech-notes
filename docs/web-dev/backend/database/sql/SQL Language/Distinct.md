
## `distinct`

```sql
SELECT DISTINCT rep_id, component_id
...
```

>[!What does distinct do?]-
> removes duplicate tuples for all the selected rows
> 
> selects all unique tuples of rep_id & component_Id

## `distinct on`

Postgres specific

it doesn't return the first tuple?????

```sql
SELECT DISTINCT ON (col1, col2)
  col3
...
ORDER BY (col1, )
LIMIT 1
```

>[!What distinct on does]
>1. Run the query
>2. At the end, GROUP BY the `ON (col)`

usually have `LIMIT 1` at the end