
## Python pre-commit

## Formatting with `black`

[GitHub - psf/black: The uncompromising Python code formatter](https://github.com/psf/black)

-   In the root of the project
    -   Create a file called: `pyproject.toml`
    -   to configure the `Black` formatter
-

```toml
[tool.black]
include = '^/c1130/.*/*\.py$'
extend-exclude = '/migrations/'
line-length = 120
```



### Sorting import

[isort](https://pycqa.github.io/isort/)

[Integrating isort with PyCharm](https://github.com/PyCQA/isort/issues/258#issuecomment-95675882)

