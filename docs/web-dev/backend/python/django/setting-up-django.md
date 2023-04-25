# Setting up Django

## Setting up locally

1. [Creating a virtual env from scratch](python-virtual-environments.md#create-a-virtual-env)
2. `pipenv install django`
3. [PyCharm setup](https://www.jetbrains.com/help/pycharm/running-manage-py.html#intro)

## Deploying Django

Python Anywhere only has MySQL for free (no Postgres 😢)

```bash
brew install flyctl
flyctl auth signup
flyctl auth login
```
