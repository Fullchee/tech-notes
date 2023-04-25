[Performing raw SQL queries](https://docs.djangoproject.com/en/dev/topics/db/sql/)

This prevents SQL injection

## Manager.raw

```python
for p in Person.objects.raw('SELECT * FROM myapp_person WHERE last_name = %s', [lname])
	print(p)
```



## [Direct database](https://docs.djangoproject.com/en/dev/topics/db/sql/#executing-custom-sql-directly)

```python
from django.db import connection

with connection.cursor() as cursor:
        cursor.execute("SELECT foo FROM bar WHERE baz = %s", [self.baz])
        row = cursor.fetchone()
        rows = cursor.fetchall()
```

```python
def dictfetchall(cursor):
    "Return all rows from a cursor as a dict"
    columns = [col[0] for col in cursor.description]
    return [
        dict(zip(columns, row))
        for row in cursor.fetchall()
    ]
```

### Using SQLAlchemy to help with raw SQL

[SQLAlchemy Tutorial](https://docs.sqlalchemy.org/en/14/core/tutorial.html#using-textual-sql)

```python
import sqlalchemy
from sqlalchemy.dialects import postgresql

statement = sqlalchemy.text(text)  # sqlalchemy.sql.elements.TextClause

# :my_var_name -> %(my_var_name)s
result = str(statement.compile(dialect=postgresql.dialect()))
```