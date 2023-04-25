# `unittest`

[`unittest` docs](https://docs.python.org/3/library/unittest.html)

-   [unittest-patch](unittest-patch.md)

The internet seems to like `pytest` more than `unittest`

-   `unittest` is like Java

## [Django testing](django-testing.md)

-   Django uses `unittest` by default

## Helper methods

[What are the differences between setUpClass, setUpTestData and setUp in TestCase class? - Stack Overflow](https://stackoverflow.com/a/43594694/8479344)

### [`setUpTestData`](https://docs.djangoproject.com/en/4.1/topics/testing/tools/#django.test.TestCase.setUpTestData)

more performant than `setUpClass`

```python
class Test(TestCase):
	@classmethod
	def setUpTestData(cls):
		pass

```

## [`mock.patch`](unittest-patch.md)

## Expecting an Exception

```python
self.assertRaises(ExceptionType, func, arg1, arg2)
```

```python
self.assertRaises(ExceptionType, lambda: func(kwarg1="a", kwarg2="b"))
```
