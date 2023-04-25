# Database Indexes

## Resources

-   https://use-the-index-luke.com/
-   [Reminders video](https://fullchee-reminders.netlify.app/link/373)

<iframe width="560" height="315" src="https://www.youtube.com/embed/HubezKbFL7E?start=74" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Why indexing

-   Faster reads and queries
-   slow queries are a common reason why websites are slow
    -   slow websites -> less profit

## Analogy for index

![dictionary-index.png](dictionary-index.png)

like tabs of a nice dictionary

links to the page, has no other info other than the first letter

## Key vs Index

Index: data structure

-   keys aren't necessarily indexed
    -   example: all the column fields form a key
    -   key: list of columns that uniquely identify any row

Primary key is always indexed

## What an index looks like

b-tree!

![what-an-index-looks-like.png](what-an-index-looks-like.png)

It will only have the data in the index

## Downsides of an index

Downside to database indices

1. Work to maintain the index 2. reads are slower 3. or you have to defrag/reindex
2. CREATE INDEX is expensive
    1. especially on a large table
3. Extra space 4. b trees and hash tables 5. some indexes can be huge, especially if the table is huge

## Secondary indexing

Student(year, major)

sort by birthday

useful if your queries are like

```sql
SELECT *
FROM Student s
WHERE s.year = 2021 AND major = 'Computer Science'
```

Not useful if you have a query like

Data not sorted wrt secondary index

so it has to do a sequential scan

```sql
SELECT *
FROM Student s
WHERE major = 'Computer Science'
```

## Date indexes

Problem with this query

Table is indexed on created_at

```sql
SELECT SUM(total)
FROM orders
WHERE YEAR(created_at) = 2013;
```

can't use created_at index because it's only indexed on the raw dates

### `psql` solution

create an index on YEAR(created_at)

### non `psql` solution

```sql
CREATE INDEX total_created_at_index ON orders(created_at, total;
```

```sql
-- ...
WHERE created_at BETWEEN January 1, 2013 AND December 31, 2013
```

## Types of indexes

Cluster index????
