# [Django Querying](https://docs.djangoproject.com/en/4.1/topics/db/queries/)

[[Django Raw SQL Queries]]

## Get

```python
try:
    user = User.objects.get(name="name")
except User.DoesNotExist:
    do_something()
```

You should use `filter` if you want to get multiple objects

```python
result = User.objects.filter(name="name")
if not result:
    do_something()
user = result.first()
```

### [`get_or_create()`](https://docs.djangoproject.com/en/3.2/ref/models/querysets/#get-or-create)

```python
obj, created = Person.objects.get_or_create(
    first_name='John',
    last_name='Lennon',
    defaults={'birthday': date(1940, 10, 9)},
)
```

## Filtering

### SQL `where id in [1,3,4,5,6....];`

```python
.filter(id__in=[1, 3, 4, 5, 6....])
```

```python
model_name.filter().values()
```

### `.filter(id=1, name=1)` vs `.filter(id=1).filter(name=1)`

[Chaining multiple filter() in Django, is this a bug? - Stack Overflow](https://stackoverflow.com/a/28253623/8479344)

-   they only might be different when dealing with foreign keys

### [Q Objects](https://docs.djangoproject.com/en/4.1/topics/db/queries/#complex-lookups-with-q-objects)

Useful for `OR` in your `WHERE` clause

Django 4.1 added `XOR`

-   `.objects.filter(a=1, b=1)` `AND`s things together

```sql
SELECT *
FROM Poll
WHERE question LIKE "Who%" OR question LIKE "What%"
```

```python
from django.db.models import Q

lookup = Q(question__startswith='Who') | Q(question__startswith='What')
Poll.objects.filter(lookup)
```

### [F Expressions](https://docs.djangoproject.com/en/4.1/ref/models/expressions/#f-expressions)

Field Expression

Get the value of that column

```sql
SELECT price * 1.13
FROM Product
```

```python
from django.db.models import F
Product.objects.filter(taxed_price=F('price') * 1.13)
```


#### Order by DESC

```sql
SELECT *
FROM Product
ORDER BY name DESC;
```

```python
Product.objects.all().order_by('-name')
```

#### Order by Nulls Last

[Query Expressions | Django Docs](https://docs.djangoproject.com/en/3.2/ref/models/expressions/#using-f-to-sort-null-values)

```sql
SELECT *
FROM Product
ORDER BY name DESC NULLS LAST;
```

```python
from django.db.models import F
Product.objects.all().order_by(F('name').desc(nulls_last=True))
```

## Subqueries

[Subqueries](https://docs.djangoproject.com/en/4.1/ref/models/expressions/#subquery-expressions)


## Get the instances from a QuerySet?

-   Convert it into a list and it will make the database call

```python
list(Widget.objects.filter())
```

UUIDField as primary key

-   cluster index?
    -   don't use UUIDs

## Choices (Django 2)

```python
  AGE_RATING =[
    ("G","General Audiences"),
    ("PG","Parental Guidance Suggested"),
    ("PG-13","Inappropriate for Children Under 13" ),
    ("R", "Restricted"),
    ("NC-17","Adults Only"),
  ]

age_rating = models.CharField(max_length= 5, choices = AGE_RATING, default = "GENERAL AUDIENCE")
```

### Choices (Django 3)

## [Aggregation](https://docs.djangoproject.com/en/4.1/topics/db/aggregation/)

To use the aggregation functions, you need

```sql
SELECT SUM(population)
FROM City
```

```python
from django.db.models import Sum, Min, Max, Avg

>>> City.objects.aggregate(Sum('population'))
{'population_sum': 1234567}
```

### Annotation

Adding a new column to the result

```sql
SELECT population * 1.05 AS "future_population"
FROM City
```

```python
>>> result = City.objects.annotate(future_population=F('population') * 1.05)
>>> result.future_population
12345
```

### `select_related`

Inner join for a `1 → n` foreign key

Fetch the foreign keys

```python
Order.objects.select_related('customer').all()
```

```sql
SELECT *
FROM Order o
  INNER JOIN Customer c
    ON (o.customer_id = c.customer_id)
```

### `prefetch_related`

Many to Many relationship

```python
Order.objects.prefetch_related('products').all()
```

`OrderProduct` is the many to many Order ↔ Product table

```sql
WITH order_ids AS (
  SELECT id
  FROM Order
)
SELECT *
FROM Product
  INNER JOIN OrderProduct
    ON Product.id = OrderProduct.product_id
WHERE OrderProduct.order_id IN (SELECT id FROM order_ids)
```

## [Many-to-many](https://docs.djangoproject.com/en/4.1/topics/db/examples/many_to_many/)

### Create an entry in a many

```python
my_obj.categories.add(fragmentCategory.objects.get(id=1))
```

```python
my_obj.categories.create(name='val1')
```

```python
my_obj.categories.add(fragmentCategory.objects.get(id=1))
```

### List many to many

```python
user.groups.all()
```


## Updating

[django post_save signals on update](https://stackoverflow.com/a/35238823/8479344)

Calls `post_save` signal

```python
user = User.objects.get(id=1) 
user.username='edited_username' 
user.save()
```


Doesn't call `post_save` signal
- converted directly into SQL

```python
User.objects.filter(id=1).update(username='edited_username')
```