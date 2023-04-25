```sql
with nums as (
    SELECT GENERATE_SERIES(1, 5) AS num
)

select ARRAY [6,7,8] && (
        select ARRAY_AGG(num)
        from nums
    )
```

```sql
with nums as (
    SELECT GENERATE_SERIES(1, 5) AS num
)

select ARRAY [1,2,3] && (
        select ARRAY_AGG(num)
        from nums
    )
```