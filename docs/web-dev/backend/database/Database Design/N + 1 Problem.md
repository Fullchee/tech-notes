Usually an issue for ORMs

[Django and the N+1 Queries Problem](https://scoutapm.com/blog/django-and-the-n1-queries-problem)

Example: printing all book titles

```python
books = Book.objects.all()
for book in books:
    print(f"{book.title} by {book.author.name}")
```



results in these queries

```sql
SELECT *
FROM books
```

N queries that look like this

```sql
SELECT *
FROM author
WHERE id = ?
```

## Solutions

### SQL

Use a view or a join

```sql
WITH books AS (
  SELECT *
  FROM authors
)
```


### Django

does ths

- [[Django ORM#`select_related`]]
- [[Django ORM#`prefetch_related`]]

### GraphQL

- [dataloader](https://github.com/graphql/dataloader)