# Python Custom Classes

## Decorators

### `@classmethod`

-   the first param is the class
-   instead of `self` (which is the instance)
    -   which accesses the instance values
    -   or class values if it hasn't been overridden
- 

```python
class Test(TestCase):
	@classmethod
	def setUpTestData(cls):
		pass

```

## Creating unique values

[Unique sentinel values, identity checks, and when to use object() instead of None](https://treyhunner.com/2019/03/unique-and-sentinel-values-in-python/)

[[spot-the-bug#The problem with None in Python]]

### `object()`

kinda Like JS Symbol

No two symbols are the same

Useful for creating unique values

```python
>>> x = object()
>>> y = object()
>>> x == y
False
```

> Every class in Python has a base class of `object`

#### [When to use `object`?](https://treyhunner.com/2019/03/unique-and-sentinel-values-in-python/#So_when_would_we_use_object()?)

1.  **Unique initial values**: a starting value that should be distinguished from values seen later (`default` and `initial` in our `min` function)
2.  **Unique stop values**: a value whose presence tells us to stop looping/processing (a true sentinel value, as in `strict_zip`)
3.  **Unique skip values**: a value whose presence should be treated as an empty value to be skipped over (we didn’t see this, but it comes up with utilities like `itertools.zip_longest` sometimes)

### Enum

[Python Enum Docs](https://docs.python.org/3/library/enum.html)

[Enums are unique values](https://treyhunner.com/2019/03/unique-and-sentinel-values-in-python/)

#### Regular enum

```python
from enum import Enum

class Color(Enum):
	RED = 1
	GREEN = 2
	BLUE = 3

>>> Color.RED
<Color.RED: 1>

>>> Color.RED.name
'RED'

>>> Color.RED.value
1
```

#### string enum

```python
from enum import Enum

class Color(str, Enum):
    GREEN: '#00ff00'

Color.GREEN == '#00ff00'
```

same thing with `IntEnum` (a built-in)
