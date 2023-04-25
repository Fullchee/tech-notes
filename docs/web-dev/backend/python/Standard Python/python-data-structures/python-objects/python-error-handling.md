# Python Error handling

## Errors keep on going up until it gets caught

```python
try:
    try:
        raise IndexError()
    except IntegrityError:
        print("Doesn't run")
except IndexError:
    print("Runs because it goes up until it gets caught")
```

## [Context Manager](https://realpython.com/python-with-statement/#creating-function-based-context-managers)

### Create your own context manager

```python
with open('hello.txt', 'w') as f:
    f.write('hello')
```

same as

```python
f = open('hello.txt', 'w')
try:
    f.write('hello')
finally:
    f.close()
```

#### Create your own class

-   implement `__enter__` and `__exit__`

```python
class ManagedFile:
    def __init__(self, name):
        self.name = name
    def __enter__(self):
        self.file = open(self.name, 'w')
        return self.file  # the return value; ManagedFile() as f
    def __exit__(self, exception_type, exception_value, exception_traceback):
        if self.file:
            self.file.close()
```

```python
with ManagedFile('hello.txt') as f:
    f.write('hello')
```

#### Using the `contextmanager` generator

```python
from contextlib import contextmanager

@contextmanager
def managed_file(name):
    try:
        f = open(name, 'w')
        yield f  # gives f back to the caller, then can do f.write('hello')
    finally:
        f.close()
```

### Python Tricks Page 33 context manager exercise

```python
with Indenter() as indent:
    indent.print('hi!')
    with indent:
        indent.print('hello')
        with indent:
            indent.print('bonjour')
    indent.print('hey')
```

Should give

```python
hi!
    hello
        bonjour
hey
```

```python
class Indenter:
    def __init__(self):
        self.indents = -1
    def __enter__(self):
        self.indents += 1
        return self
    def __exit__(self, exception_type, exception_value, exception_traceback):
        self.indents -= 1
    def print(self, string):
        tab = "\t"
        print(f'{tab * self.indents}{string}')
```

### Python Tricks Page 35 context manager

-   context manager that measures the execution time of a code block using the `time.time` function

### Context managers vs decorators

-   separate concepts
-   `contextlib.contextmanager` lets your context managers be decorators
    -   so you don't need to use `with`

## [`suppress`](https://docs.python.org/3/library/contextlib.html#contextlib.suppress)

Cleaner version of `try/except` and ignore

```python
from contextlib import suppress

with suppress(FileNotFoundError):
    os.remove('somefile.tmp')
```

same as

```python
try:
    os.remove('somefile.tmp')
except FileNotFoundError:
    pass
```

## Get the error message from an exception

-   no standard property
-   use `str(e)`
-   or debug and get the properties for that specific Exception
    -   `error_message = e.detail["name"][0]`

