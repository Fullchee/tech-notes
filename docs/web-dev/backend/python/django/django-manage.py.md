# Django `manage.py` scripts

[Write your own commands](https://docs.djangoproject.com/en/dev/howto/custom-management-commands/)

## Creating your custom commands

1. Create a file called: `app_name/management/commands/create_admin_superuser.py`
2. Fill in the blanks

### Example

```python
from django.core.management.base import BaseCommand

class Command(BaseCommand):
    help = """ help string """

    def add_arguments(self, parser):
        parser.add_argument("email", type=str)
        parser.add_argument("password", type=str)

    def handle(self, *args, **options):
        # do stuff
        self.stdout.write("Created an admin superuser")
```

## Python Shell

```sh
python manage.py shell
```

```python
import django
django.setup()
from django.contrib.auth.models import User, Group
# other imports
```

`manage.py shell` vs `python` console

-   `manage.py shell` sets the `DJANGO_SETTINGS_MODULE`which lets it know about the `settings.py`

(`django_extensions` has a `shell_plus`)

## [`django_extensions`](https://github.com/django-extensions/django-extensions)

[video](https://vimeo.com/1720508?embedded=true&source=vimeo_logo&owner=627770)

adds a bunch of nice helpers to `./manage.py`

-   `graph_models`
    -   graphs your models
-   `runserver_plus`
    -   django error page with a Python terminal to see the info
-   `runscript`
    -   run a python file that sets up django (import django, django.setup())
    -   nice for scripts that are run with cron
-   `shell_plus`
    -   django shell that loads all of your models
-   `print_user_for_session <session_ID>`
    -   get all of the session info for a user
