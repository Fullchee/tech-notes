
Manage [[Django Models]]

https://docs.djangoproject.com/en/dev/ref/contrib/admin/

You don't need to create a `class <Model>Admin`!

```python title="<app>/admin.py"
from django.contrib import admin
from myapp.models import Author

admin.site.register(Author)
```

## Using a `ModelAdmin`

```python title="admin.py"

class SecurityUserModelAdmin(admin.ModelAdmin):
```


## Creating your own `ModelAdmin`

You can override the default `ModelAdmin`

-   you can create a custom `ModelAdmin`
- that always has the buttons the top for example
	- Forma

```python
class MyModelAdmin(admin.ModelAdmin):
    save_on_top = True
```

Then using it in `admin.py`


### Use `<input type="text">` instead of `<textarea>` for `TextField`

```python
from django.db.models import TextField
from django.forms import TextInput
from django.contrib.admin import ModelAdmin

class PageAdmin(ModelAdmin):

    formfield_overrides = {
        TextField: {"widget": TextInput},
    }
```


### Link a foreign key

```python title="admin.py"
from django.contrib import admin
from django.urls import reverse  
from django.utils.html import format_html

@admin.register(Dashboard)
class DashboardAdmin(admin.ModelAdmin):
    list_display = (
        ...
        # column header name
        "go_to_permission",
    )

    @staticmethod
    def go_to_permission(dashboard):
        url = reverse("admin:permissions_configurator_permission_change", args=[dashboard.permission.id])
        return format_html('<a href="{}">{}</a>', url, dashboard.permission.name)
```

[Reversing Admin URLs](https://docs.djangoproject.com/en/3.2/ref/contrib/admin/#reversing-admin-urls)

![[image-20221122133051604.png]]

## Prevent deletion in Django admin

[In Django Admin how do I disable the Delete link - Stack Overflow](https://stackoverflow.com/a/25813184/8479344)