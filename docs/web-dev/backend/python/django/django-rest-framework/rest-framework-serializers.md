# [DRF Serializers](https://www.django-rest-framework.org/api-guide/serializers/)

> [!danger]
> Don't use DRF Serializers to create model instances!
> [[Scaling Django - Where to put business logic]]

Nested model

```python
Dashboard
    name
    pages
```

```python
Pages
    name
    widgets
```

```python
Widgets
    name
```

## Deserializing (usage)

Database to JSON

```python
dashboards = DashboardSerializer(
    Dashboard.objects.all(),
    many=True)
.data
```

## Creating the Serializer

[SerializerMethodField](https://www.django-rest-framework.org/api-guide/fields/#serializermethodfield)

-   return anything you want in the serializer data
-   read-only
    -   use a [`CustomField`](https://www.django-rest-framework.org/api-guide/fields/#custom-fields) if you want read/write
- 

```python
class DashboardSerializer(serializers.ModelSerializer):
    dashboard_pages = serializers.SerializerMethodField("get_dashboard_pages")
    # just want an array of pages?
    # dashboard_pages = PageSerializer(many=True)

    class Meta:
        model = Page
        fields = ("id", "name", "dashboard_pages")

    def get_dashboard_pages(self, dashboard: Dashboard):
        page_query_set = Page.objects.filter(dashboard=dashboard)
        pages = PageSerializer(page_query_set, many=True, read_only=True).data
        return {page["id"]: page for page in pages}
```

## [Serializing](https://www.django-rest-framework.org/api-guide/serializers/#saving-instances)

JSON to database

### Code in `view.py`

```python
try:
    dashboard = Dashboard.objects.get(id=id)
except Dashboard.DoesNotExist:
    pass

# updates if you pass an instance of the model
# DashboardSerializer(data=data) to create
serialized_dashboard = DashboardSerializer(dashboard, data=data)
if serialized_dashboard.is_valid(raise_exception=True):
    serialized_dashboard.save()  # triggers serializer update() or create()
```



### `update()`

```python
def update(self, instance: Dashboard, validated_data: dict):
    instance.name = validated_data.get("name", instance.name)
    instance.save()

    for page_data in pages:
        page = Page.objects.get(id=page_data["id"])
        serialized_page = PageSerializer(page, data=page_data)
        if serialized_page.is_valid(raise_exception=True):
            serialized_page.save()
```

### [Overriding `.save()` directly](https://www.django-rest-framework.org/api-guide/serializers/#overriding-save-directly)


### What is `validated_data`

When you pass in some data

```python
DashboardSerializer(dashboard, data=data)
```

Django Rest Framework by default strips all of the properties that are

-   read-only
-   not listed in the `fields` of the serializer

#### Update a `1 to 1` foreign key

```
DashboardWidget <-> DashboardQuery
```

`DashboardWidget.query_file_path`

-   string foreign key to `DashboardQuery`
-   need to set the model

```python
instance.query = DashboardQuery.objects.get(file_path=file_path)
```

because we can't do `.update()` because we're given the instance and not a query set

#### How do I add custom field to the `validated_data`?

add values to 

```python
DashboardSerializer(data=data).save(name="my_dash")

# dynamic values
key_name = "name"
.save(**{key_name: "my_dash"})
```

?????

TODO: I don't know what `to_internal_value` does

implement your own `to_internal_value`

```python
def to_internal_value(self, data):
	# `data` <=> `self.initial_data`
    if not data.get("query_file_path"):  
        data["query_file_path"] = None  
    return super().to_internal_value(data)
```

## [Custom fields](https://www.django-rest-framework.org/api-guide/fields/#a-basic-custom-field)

```python
class ColorField(serializers.Field):
    """
    Color objects are serialized into 'rgb(#, #, #)' notation.
    """
    def to_representation(self, value):
        return "rgb(%d, %d, %d)" % (value.red, value.green, value.blue)

    def to_internal_value(self, data):
        data = data.strip('rgb(').rstrip(')')
        red, green, blue = [int(col) for col in data.split(',')]
        return Color(red, green, blue)
```

https://github.com/beda-software/drf-writable-nested

Custom fields are for serialization or deserialization

If you want a custom nested field that does something like

PageSerializer(many=True)

Except it can return anything you want, ???
