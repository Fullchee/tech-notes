# Python logging

## Code

```python
import logging

logger = logging.getLogger(__name__)
logger.info("My message")
```

## Error levels

Info levels
- INFO

-   **INFO:** general info
-   **WARNING:** Minor problem
	- still info, give more details when debugging
-   **ERROR:** Major problem
	- something's broken! high priority
-   **CRITICAL:** Critical problem
	- system as as whole is down


## `warnings` module

[Fullchee Values](https://fullchee-reminders.netlify.app/link/2161)

warns devs, not end users

### Using `warnings` module

Useful for deprecation notices

`stacklevel` should be 2+
- default `stacklevel` is 1
- not helpful, doesn't say who called the module

```python
import warnings

def old_func():
	warnings.warn(
		DeprecationWarning('use new_func instead'),
		stacklevel=2
	)
```

```bash
$ PYTHONWARNINGS=once python3 file.py

$ python3 -Wonce file.py

$ python3 -Werror file.py
```


### [`logging.warning` vs `warnings.warn`](https://stackoverflow.com/questions/9595009/warnings-warn-vs-logging-warning/14762106#14762106)

-   `logging.warning`
    -   issue with input/user
    -   nothing the client app can do
-   `warnings.warn`
    -   dev issue
        -   examples
            -   deprecated code
            -   abstract class not implement

## Adding a traceback

[log stack trace](https://stackoverflow.com/questions/5191830/how-do-i-log-a-python-error-with-debug-information/5191885#5191885)

can only be in an `except` clause

- otherwise you get an error

```python
except Exception as e:
	logger.exception("Exception message")
```

Shorthand for

```python
logger.error("something weird happened", exc_info=True)
```

- `exc_info=True` is useful if you want to log an error

## Deprecated warning

```python
warnings.warn(
			  "message",
			  category=DeprecationWarning,
)
```


## Tips on logging message

- multiple machines?
	- include a request ID so all logs can be grouped
- per user
	- easily debug a user specific issue
