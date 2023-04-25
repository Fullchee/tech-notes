# [Python decorators](https://realpython.com/primer-on-python-decorators/)

## `functools.wraps`

```python
import functools

def do_twice(func):
    @functools.wraps(func)
    def wrapper_do_twice(*args, **kwargs):
        func(*args, **kwargs)
        return func(*args, **kwargs)
    return wrapper_do_twice
```

### Class decorators

Need `updated=()`

```python
import functools
def dec(cls):
	@functoosl.wraps(cls, updated=())
	class Wrapper(cls):
		pass

	return D
```

## Order of decorators

```python
@decorator2
@decorator1
def my_fn():
    pass
```

Expands outwards

`decorator2(decorator1(my_fn()))`
