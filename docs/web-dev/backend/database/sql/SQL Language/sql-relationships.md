# SQL Relationships

## Foreign Keys

### `ON DELETE CASCADE`

[sql - PostgreSQL: FOREIGN KEY/ON DELETE CASCADE - Stack Overflow](https://stackoverflow.com/a/33807220/8479344)

Deleting any `clan` (the other table) will delete any `hobbit`s

If you delete a `hobbit` (current table), nothing will happen to the other table

-   unless there's a many-to-many relationship

```sql
CREATE TABLE clan (
    id serial PRIMARY KEY,
    clan varchar
);

CREATE TABLE hobbit (
    id serial PRIMARY KEY,
    hobbit varchar,
    clan_id integer REFERENCES shire.clans (id) ON DELETE CASCADE
);
```



## [Are two tables the same?](https://dba.stackexchange.com/questions/72641/checking-whether-two-tables-have-identical-content-in-postgresql)


```sql
SELECT CASE WHEN EXISTS (TABLE a EXCEPT TABLE b)
              OR EXISTS (TABLE b EXCEPT TABLE a)
            THEN 'different'
            ELSE 'same'
       END AS result ;
```