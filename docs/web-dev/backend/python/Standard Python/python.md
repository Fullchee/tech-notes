## TODOs

-   [Python glossary](https://docs.python.org/3/glossary.html)
-   How I've gotten better at Python
    -   Python Tricks
        -   Dan Bader of RealPython
    -   Python Morsels
        -   Trey Hunner weekly emails
-   Keep up to date
    -   [Python Bytes: Python headlines](https://pythonbytes.fm/)

## Functions

### Forced name params

-   pass a `*` to separate positional args and keyword args

```python
def foo(pos, *, forcenamed, **kwargs):
    pass

my_func(1, 2) # throws an error
```

### Mark a function as deprecated

-   https://github.com/tantale/deprecated
-   decorator

### Garbage collection

```python
def yell():
    pass

bark = yell

del yell  # only deletes one pointer to the function

bark()  # still in the heap because there's still one pointer left
```

## File system

### Path

```python
from pathlib import Path

file_directory = Path(__file__).parent.resolve()
another_path = file_directory / "sql_scripts"
```

### Get an environment variable value

```python
os.environ.get('ENV_VAR_NAME', 'FALLBACK_VALUE')
```

`os.getenv()` is an alias to `os.environ.get()`

## Equality

### `==` vs `is`

-   `is`: same ID
	- place in the stack/heap
	- `id(x) => 140079600030400`
-   `==`: uses `__eq__`
	- by default, `==` delegates to `is`

### [`isinstance` vs `type()`](https://stackoverflow.com/a/1549854/8479344)

-   `type`: returns the name of the type
-   `isinstance([1,2,3], list)`
    -   goes up the inheritance tree
    -   can catch more than comparing two `type`s

### [walrus operator](https://fullchee-reminders.netlify.app/link/1945)

```python
match = MY_REGEX.search(string)
if match:
    pass
```

```python
if match := MY_REGEX.search(string):
    pass
```

```python
while chunk := f.read(8192):
    md5.update(chunk)
```

-   new in Python 3.8
-   assignment expression
    -   merge two lines into one
-   assignment statements needs to be on their own line
-   **When to use?**
    -   only if it makes your code more readable



## Random

### Pseudorandom

```python
import random
>>> colors = ['blue', 'purple', 'green', 'yellow']
>>> random.choice(colors)
'purple'
```

### Closer to true random

```python
import secrets
secrets.choice(colors)
```
