# Python virtual environment tools

Old tools

-   Virtualenv
    -   Supports Python 2
-   venv
    -   In Python 3 stdlib
    -   Basically the same as virtualenv

New tools

-   pipenv
-   poetry
-   pdm
    -   Uses the py\_\_\_.toml

## pyenv

-   Not a virtual environment
-   download the right version of python

## `pipenv`

### why `pipenv`

-   managed by pypa
    -   python packaging authority
    -   same people who manage
        -   pip
        -   virtualenv
        -   wheel

### Enter the virtual env

```bash
pipenv shell
```

## Create a virtual env

1. Install the version of Python you wanna use 2. `pyenv install --list` 3. list all version of Python `pyenv` cn install 4. `pyenv install 3.10.6`
2. Switch to that version of python 6. `pyenv local 3.10.6`
3. Setup the env with that version of python 5. `pipenv install --python 3.10.6` 6. `pipenv install` to install with your current version


### Create a `pipenv` env from `requirements.txt`

[`pipenv install` throws `--system is intended to be used for pre-existing Pipfile installation` · Issue #5052 · pypa/pipenv · GitHub](https://github.com/pypa/pipenv/issues/5052#issuecomment-1108872335)

`pipenv install`

> Your dependencies could not be resolved. You likely have a mismatch in your sub-dependencies.
