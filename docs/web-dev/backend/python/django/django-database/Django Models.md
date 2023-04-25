# Django Models

## [[Django Admin]]

https://betterprogramming.pub/everything-you-need-to-know-about-django-models-in-python-2a44ed4293dd

`__str__` : used in template
- ???? template?

Choices (Django 3)

Validators

## [Querying models (Django ORM)](Django%20ORM.md)

## Creating model fields

### [`null=True` vs `blank=True`](https://stackoverflow.com/questions/8609192/what-is-the-difference-between-null-true-and-blank-true-in-django)

-   `blank=True` can leave it blank for forms
    -   example: Django admin form
-   `null=True` the value in the table can be `NULL`

### Foreign Keys

#### Set a foreign key to be something other than an ID

```python
class DashboardWidget(models.Model):
    query = models.ForeignKey(
        DashboardQuery,  # the foreign model
        to_field="file_path",  # DashboardQuery.file_path, must be unique
        db_column="query_file_path",  # name of the db column, default: query_id (field-name_id)
        related_name=""
        ...
    )
```

#### `ForeignKey.related_name`

[What is related_name used for?](https://sentry.io/answers/what-is-related-name-used-for/)

```python
from django.db import models

class Author(models.Model):
    name = models.CharField(max_length=200)

class Book(models.Model):
    author = models.ForeignKey(Author, on_delete=models.CASCADE)
    title = models.CharField(max_length=200)
```

##### Default related_name
```python
>>> alex = Author.objects.get(name="Alex Smith")
>>> alex_books = Book.objects.filter(author=alex)
```

> [!Equivalent using `related_name`]-
> 
> ```python
> >>> alex = Author.objects.get(name="Alex Smith")
> >>> alex_books = alex.book_set.all()
> ```

> [!What would it look like if `related_name=books`]-
> ```diff
> alex_books = alex.
> - book_set.all()
> + books.all()
> ```


Doing a migration?

-   you need to drop the `DashboardWidget.query` and then re-create it
-   `AlterField` doesn't change the column type from `int` to `text` in Django 2.2



### Enums in Models

You can also create a subclass for more precision
[Model Enum Types](https://docs.djangoproject.com/en/dev/ref/models/fields/#enumeration-types)


```python
class Dashboard(models.Model):
    class Status(models.TextChoices):
        ACTIVE = "active"
        DRAFT = "draft"

    status = models.CharField(
	    max_length=6,
	    choices=Status.choices,
	    default=Status.DRAFT
	)
```

```python
>>> Dashboard.Status.DRAFT
<Status.DRAFT: 'draft'>
```

Shorthand

```python
MedalType = models.TextChoices('MedalType', 'GOLD SILVER BRONZE')
>>> MedalType.choices
[('GOLD', 'Gold'), ('SILVER', 'Silver'), ('BRONZE', 'Bronze')]

status = models.CharField(
	    max_length=6,
	    choices=Status.choices,
	    default=Status.DRAFT
	)
```

## Validating objects

[Django docs: Validating objects](https://docs.djangoproject.com/en/4.1/ref/models/instances/#validating-objects)


`.clean()`
????

## Model properties

[Django-Styleguide#properties](https://github.com/HackSoftware/Django-Styleguide#properties)

- simple derived

```python
from django.utils import timezone
from django.core.exceptions import ValidationError

class Course(BaseModel):
    name = models.CharField(unique=True, max_length=255)

    start_date = models.DateField()
    end_date = models.DateField()

    def clean(self):
        if self.start_date >= self.end_date:
            raise ValidationError("End date cannot be before start date")

    @property
    def has_started(self) -> bool:
        now = timezone.now()

        return self.start_date <= now.date()

    @property
    def has_finished(self) -> bool:
        now = timezone.now()

        return self.end_date <= now.date()

	# method
    def is_within(self, x: date) -> bool:
        return self.start_date <= x <= self.end_date
```

## Migrations

### Create an empty migration

useful when you're creating a custom migration

```shell
python manage.py makemigrations app_name --name migration_name --empty
```

### Create a migration

operations list

```python
from django.db import migrations

class Migration(migrations.Migration):

	dependencies = [
        ('dashboard_etl_manager', '0031_previous'),
    ]

    operations = [
        migrations.RunPython(python_function_name, migrations.RunPython.noop),
		migrations.RunSQL("SELECT * FROM table", migrations.RunSQL.noop),
    ]
```

#### Reverse a migration

```python
operations = [
        migrations.RunSQL(
            'CREATE INDEX "app_sale_sold_at_b9438ae4" '
            'ON "app_sale" ("sold_at");',

            reverse_sql='DROP INDEX "app_sale_sold_at_b9438ae4";',
        ),
    ]
```

Then `python manage.py migrate app_name 0008

#### Add an index to a table that already has a ton of data in it

-   https://realpython.com/create-django-index-without-downtime/#non-atomic-migrations


