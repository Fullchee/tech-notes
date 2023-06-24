TO_CHAR()

Formatting to currency

```sql
> SELECT TO_CHAR(123456789.9876, 'FM$999G999G999.00')
'$123,456,789.99'
```

[Template Patterns & Modifiers for Numeric Formatting in PostgreSQL](https://database.guide/template-patterns-modifiers-for-numeric-formatting-in-postgresql/)


Round 

```sql
select '123.123'::DECIMAL (10, 0)
```