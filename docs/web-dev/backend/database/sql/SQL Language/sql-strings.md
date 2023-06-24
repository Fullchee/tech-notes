# SQL strings

```sql
regexp_replace(divide_lc_to_get_usd, '[a-zA-Z, ]+','','g')
```

-   remove characters, comma, and space from value

## Translate

????


## [Regex](https://www.postgresql.org/docs/current/functions-matching.html#FUNCTIONS-POSIX-REGEXP)


```sql
select 'thomas' ~ 't.*ma';
+----------+
| ?column? |
|----------|
| True     |
+----------+
```

use LIKE if possible

- `LIKE` is part of the SQL standard
- `~` is non-standard
