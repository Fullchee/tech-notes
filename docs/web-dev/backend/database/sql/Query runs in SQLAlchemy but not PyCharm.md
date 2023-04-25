>ERROR: COALESCE types text and integer cannot be matched

The default column type is `text`

Ensure that `NULL` columns have the right type

```diff
SELECT
-  NULL AS some_col
+  NUL::NUMERIC as some_col
```

