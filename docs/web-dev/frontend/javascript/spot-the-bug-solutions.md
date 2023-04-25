# Spot the bug solutions

```diff
const newsletter = "Bytes"
- const tagline = "Your weekly dose of JavaScript"
+ const tagline = "Your weekly dose of JavaScript";
[newsletter, tagline].forEach((el) => console.log(el))
```

You need a semi-colon

interpreted as

```javascript
"Your weekly dose of JavaScript"[(newsletter, tagline)].forEach();
```


## The problem with `None` in Python

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


2 bugs that stem from how we're using `None` to check for undefined both times

```python
>>> min([None], default=0)
0
>>> min([None])
ValueError: Empty iterable
```


```python
>>> min([1,2,3], default=None)
ValueError: Empty iterable
```