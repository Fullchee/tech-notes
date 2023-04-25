# Testing Django

## Related Links

### Related pages

-   [Python Testing](unittest.md)
-   [Factories](django-factories.md)
-   [Testing endpoints](django-testing-endpoints.md)
- [[Running Tests]]
	- [[faster-pycharm-tests]]

### Django docs

-   [Writing and running Django tests | Overview](https://docs.djangoproject.com/en/4.1/topics/testing/overview/)
-   `manage.py test` docs
    -   [django-admin and manage.py | Django docs](https://docs.djangoproject.com/en/4.1/ref/django-admin/#test)
-   [Advanced testing topics | Django docs](https://docs.djangoproject.com/en/4.1/topics/testing/advanced/)

## [Testing endpoints](django-testing-endpoints.md)

## Writing a basic test

#### Override settings

```python
from django.test import override_settings

class TestBuildPath(TestCase):
    @override_settings(CLIENT_ID=1130)
    def test_overriding_settings(self):
        self.assertEqual(settings.CLIENT_ID, 1130)
```

#### [`patch` and mocking](unittest.md#patch)

#### Auth

Login as a super user

```python
@classmethod
    def setUpTestData(cls):
        cls.user = UserFactory(is_superuser=True)
```

```python
self.client.force_login(self.user)
```

#### [Factories](django-factories.md)

Create mock data

### Act

-   Call the function
-   make the API call

### Assert

#### Expect raising an error

```python
self.assertRaises(ExpectedException, fn_name, arg1, arg2)
```


it also returns a context manager!

```python
from django.core.exceptions import ValidationError
with self.assertRaises(ValidationError):
	course.full_clean()
```

### No need to tear down data!

We use `django.test.TestCase`

-   inherits from the `TransactionTestCase`
-   tests are always within a database transaction
    -   which is then rolled back when the test completes

*   [Reference](https://docs.djangoproject.com/en/3.2/topics/testing/tools/#django.test.TestCase)

## Using another testing framework

override the `TEST_RUNNER` env var

### Have code that will run before the tests

```python
from django.test.runner import DiscoverRunner
from some.path import patch_feature_flags


class DefaultTestRunner(DiscoverRunner):
    def run_tests(self, test_labels, extra_tests=None, **kwargs):
        with patch_feature_flags({}):
            """ Don't get feature flag value from LaunchDarkly. """
            return super().run_tests(test_labels, extra_tests=None, **kwargs)
```

[[feature-toggles#How to test feature flags]]