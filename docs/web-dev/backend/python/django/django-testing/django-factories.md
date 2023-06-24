# Django Factories

Related links

-   [Django testing](django-testing.md)

## What

Library we use: factory_boy

-   https://factoryboy.readthedocs.io/en/stable/index.html

## Why

-   Create instances of models with realistic mock data
-   Useful when creating mock data in tests

## Example

Example model

-   [`Dashboard` ](https://github.com/forma-ai/backend-core/blob/e320eab8de1526e6540d94783bf083358e7bff96/backendcore/dashboard_etl_manager/models/load.py#L6)
    -   can have many [`Page`](https://github.com/forma-ai/backend-core/blob/e320eab8de1526e6540d94783bf083358e7bff96/backendcore/dashboard_etl_manager/models/load.py#L33)

### Without Factory

Two pages on the same dashboard

```python
from .models import Dashboard, Page

dashboard = Dashboard.objects.create(
	name="dashboard-name",
	...
)

page1 = Page.objects.create(
	name="Page name 1",
	dashboard=dashboard,
	...
)

page2 = Page.objects.create(
	name="Page name 2",
	dashboard=dashboard,
	...
)
```

### With Factory

`PageFactory` creates a dashboard if one isn't passed in

```python
page1 = PageFactory()
page2 = PageFactory(dashboard=page1.dashboard)
```

#### Creating bulk instances

```python
MyFactory.create_batch(5)
```

## Creating a Factory

`factory_boy` uses `faker` to generate mock data

-   https://faker.readthedocs.io/en/master/

```python
import factory
from faker import Faker

from .models import Page
from .factories import DashboardFactory

faker = Faker()


class PageFactory(factory.django.DjangoModelFactory):
    class Meta:
        model = ModelName

    # don't need to generate the ID if it's auto incrementing

	# o: the current instance object
    name = factory.Sequence(lambda n: f"name_{n}")
    shard = factory.LazyFunction(lambda: )

    # will generate a Dashboard if dashboard isn't provided
    dashboard = factory.SubFactory(DashboardFactory)
```

`Lazy` means that a new value will be generated for every new `Page` created by `PageFactory`

-   [`LazyFunction`](https://factoryboy.readthedocs.io/en/stable/reference.html#lazyfunction)
    -   `lambda: do_stuff`
-   [`Sequence`](https://factoryboy.readthedocs.io/en/stable/reference.html#sequence)
    -   `lambda n: n`
-   [`LazyAttribute`](https://factoryboy.readthedocs.io/en/stable/reference.html#lazyattribute)
    -   `lambda o: f"{o.id}_suffix"`
    -   `o`: the current instance object
-   [`LazyAttributeSequence`](https://factoryboy.readthedocs.io/en/stable/reference.html#lazyattributesequence)
    -   `lambda o, n: f"{o.number}_{n}"`
    -   Attribute + Sequence

>[!.create() vs .build()]-
>PageFactory() <==> PageFactory.create()
>
>PageFactory.build() doesn't call `.save()` so no database entry is created in the database
