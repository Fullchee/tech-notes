# Spot the bug



```javascript
const newsletter = "Bytes"
const tagline = "Your weekly dose of JavaScript"

[(newsletter, tagline)].forEach(
    (el) => console.log(el)
)
```




## The problem with `None` in Python

[[python-custom-classes#Creating unique values]]

[Unique sentinel values, identity checks, and when to use object() instead of None](https://treyhunner.com/2019/03/unique-and-sentinel-values-in-python/)

```python
def min(iterable, default=None):
    """Imperfect re-implementation of Python's built-in min function."""
    minimum = None
    for item in iterable:
        if minimum is None or item < minimum:
            minimum = item
    if minimum is not None:
        return minimum
    elif default is not None:
        return default
    else:
        raise ValueError("Empty iterable")
```