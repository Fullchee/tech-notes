### [Always have the `--keepdb` option in PyCharm](faster-pycharm-tests.md)
- In PyCharm click the green triangle beside a test


## Running tests in terminal

```shell
python manage.py test path.app.tests.ClassName.testName --keepdb
```

-   [**-k** flag](https://docs.djangoproject.com/en/4.1/ref/django-admin/#cmdoption-test-k): match test name patterns

```shell
python manage.py test -k match.pattern1 -k match.pattern2
```

## Code coverage

```bash
pip install coverage

# replace `python` with `coverage run`
coverage run --branch manage.py test
coverage html
```
