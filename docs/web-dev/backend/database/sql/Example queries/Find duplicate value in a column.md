
```sql
SELECT *
FROM my_table t1
WHERE EXISTS (
    SELECT 1 
    FROM my_table t2
    WHERE t1.rep_id = t2.rep_id 
    AND (t1.column1 <> t2.column1 OR t1.column2 <> t2.column2)
);
```