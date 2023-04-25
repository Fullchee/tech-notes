snapshot of the data

## Materialized view vs table

Materialized view is a table with a view linked on it

We can apply all table operations on a materialized view
- example: indexes

`REFRESH MATERIALIZED VIEW`

equivalent to

```
DROP TABLE my_table;
CREATE TABLE my_table AS (...);
```

But you can't change the schema?
