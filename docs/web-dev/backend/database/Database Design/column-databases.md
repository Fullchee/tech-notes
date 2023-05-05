# Column databases

columnar or column oriented databases

[Hussein Nasser video](https://fullchee-reminders.netlify.app/link/1756)
<iframe width="511" height="287" src="https://www.youtube.com/embed/Vw1fCeD06YI" title="Column vs Row Oriented Databases Explained" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

## Examples

- Apache Cassandra
- Sentry uses a columnar database too??
- Power BI

???

![column-database-example.png](column-database-example.png)

```sql
SELECT * FROM table WHERE id=1
```

Writes (and updates) are very slow

Writes and reads are complex

## Row vs Column database

### When to use row based

-   default, handles most cases well enough
    -   the power drill of databases
-   read & write
-   OLTP
    -   online transaction processing
    -   concurrent transactions
        -   online banking, shopping, texting
-   efficient queries with multiple columns

### When to use column database

-   data lakes and warehouses
    -   data is static
    -   need to aggregate a lot
-   when you don't have a lot of writes
-   OLAP
    -   online analytical processing
    -   business insights from data



## Power BI
- UI/display
- analysis services
	- in memory column store
	- very efficient for analytics purposes