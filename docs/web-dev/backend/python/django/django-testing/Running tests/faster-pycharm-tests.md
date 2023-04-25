# Faster Django tests in PyCharm

## [PyCharm notes](pycharm.md)

## Problem

Pressing the green play triangle button is slow.

![pycharm-triangle.png](pycharm-triangle.png)

It runs `python manage.py path_to_test`

-   drops and creates a new test database
-   (slow 🐢)

## Solution

We can update the `Django tests` template to add the `--keepdb` option

So that when you click on the green triangle, it will run

```diff
- python manage.py path_to_test
+ python manage.py path_to_test --keepdb
```

1. Open the Run/Debug Configurations
    1. In the top right of PyCharm, click the box to the left of the green play button
    2. Click `Edit Configurations...`
    3. ![edit-configurations.png](edit-configurations.png)
2. Add the `--keepdb` option to the Django tests
    1. ![2022-pycharm-tests.png](2022-pycharm-tests.png)

??? "Have an older version of PyCharm that doesn't match that screenshot?"

    Screenshot for PyCharm 2020.3

    ![pycharm-django-config.png](./images/pycharm-django-config.png)

## Apply migrations in the test database

Tests failing because your migrations aren't in the test database?

1. Get the name of your test database
    1. test database has the same name as the `DATABASE_URL` in `.env` with a `test_` prefix
    2. example
        1. database name is `my_db`
        2. the test database is `test_my_db`
2. Drop the test database
    1. `dropdb test_my_db`
3. Run a test
    1. a new database will be created with the migrations
