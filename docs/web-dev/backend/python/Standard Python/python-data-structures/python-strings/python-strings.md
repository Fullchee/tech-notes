# Python String Formatting

## String methods to memorize

| Method                                                                                                                                                                                                                                     | Related Methods     | Description                                           |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------- | ----------------------------------------------------- |
| [`join`](https://www.pythonmorsels.com/string-methods/?__s=jfol4nia3swnkqvkqg8b&utm_source=drip&utm_medium=email&utm_campaign=2022-08-31+weekly+email&utm_content=Weekly+Python+tip%3A+12+string+methods+to+remember#join)                 |                     | Join iterable of strings by a separator               |
| [`split`](https://www.pythonmorsels.com/string-methods/?__s=jfol4nia3swnkqvkqg8b&utm_source=drip&utm_medium=email&utm_campaign=2022-08-31+weekly+email&utm_content=Weekly+Python+tip%3A+12+string+methods+to+remember#split)               | `rsplit`            | Split (on whitespace by default) into list of strings |
| [`replace`](https://www.pythonmorsels.com/string-methods/?__s=jfol4nia3swnkqvkqg8b&utm_source=drip&utm_medium=email&utm_campaign=2022-08-31+weekly+email&utm_content=Weekly+Python+tip%3A+12+string+methods+to+remember#replace)           |                     | Replace all copies of one substring with another      |
| [`strip`](https://www.pythonmorsels.com/string-methods/?__s=jfol4nia3swnkqvkqg8b&utm_source=drip&utm_medium=email&utm_campaign=2022-08-31+weekly+email&utm_content=Weekly+Python+tip%3A+12+string+methods+to+remember#strip)               | `rstrip` & `lstrip` | Remove whitespace from the beginning and end          |
| [`casefold`](https://www.pythonmorsels.com/string-methods/?__s=jfol4nia3swnkqvkqg8b&utm_source=drip&utm_medium=email&utm_campaign=2022-08-31+weekly+email&utm_content=Weekly+Python+tip%3A+12+string+methods+to+remember#casefold)         | `lower` & `upper`   | Return a case-normalized version of the string        |
| [`startswith`](https://www.pythonmorsels.com/string-methods/?__s=jfol4nia3swnkqvkqg8b&utm_source=drip&utm_medium=email&utm_campaign=2022-08-31+weekly+email&utm_content=Weekly+Python+tip%3A+12+string+methods+to+remember#startswith)     |                     | Check if string starts with 1 or more other strings   |
| [`endswith`](https://www.pythonmorsels.com/string-methods/?__s=jfol4nia3swnkqvkqg8b&utm_source=drip&utm_medium=email&utm_campaign=2022-08-31+weekly+email&utm_content=Weekly+Python+tip%3A+12+string+methods+to+remember#endswith)         |                     | Check if string ends with 1 or more other strings     |
| [`splitlines`](https://www.pythonmorsels.com/string-methods/?__s=jfol4nia3swnkqvkqg8b&utm_source=drip&utm_medium=email&utm_campaign=2022-08-31+weekly+email&utm_content=Weekly+Python+tip%3A+12+string+methods+to+remember#splitlines)     |                     | Split into a list of lines                            |
| [`format`](https://www.pythonmorsels.com/string-methods/?__s=jfol4nia3swnkqvkqg8b&utm_source=drip&utm_medium=email&utm_campaign=2022-08-31+weekly+email&utm_content=Weekly+Python+tip%3A+12+string+methods+to+remember#format)             |                     | Format the string (consider an f-string before this)  |
| [`count`](https://www.pythonmorsels.com/string-methods/?__s=jfol4nia3swnkqvkqg8b&utm_source=drip&utm_medium=email&utm_campaign=2022-08-31+weekly+email&utm_content=Weekly+Python+tip%3A+12+string+methods+to+remember#count)               |                     | Count how many times a given substring occurs         |
| [`removeprefix`](https://www.pythonmorsels.com/string-methods/?__s=jfol4nia3swnkqvkqg8b&utm_source=drip&utm_medium=email&utm_campaign=2022-08-31+weekly+email&utm_content=Weekly+Python+tip%3A+12+string+methods+to+remember#removeprefix) |                     | Remove the given prefix                               |
| [`removesuffix`](https://www.pythonmorsels.com/string-methods/?__s=jfol4nia3swnkqvkqg8b&utm_source=drip&utm_medium=email&utm_campaign=2022-08-31+weekly+email&utm_content=Weekly+Python+tip%3A+12+string+methods+to+remember#removesuffix) |                     | Remove the given suffix                               |

## String formatting

https://www.pythonmorsels.com/string-formatting/

### `f` strings

#### f-string debugging

Prints out both the var name and the value

```python
>>> python = 3.8
>>> f"{python=}"
'python=3.8'
```

#### Formatting numbers

```python
>>> p = 0.374
>>> print(f"{p:.1%} full")
37.4% full
```

| Output     | f-string field |
| ---------- | -------------- |
| '4125.60'  | `{n:.2f}`      |
| '4,125.60' | `{n:,.2f}`     |
| '04125.60' | `{n:08.2f}`    |
| '37%'      | `{p:.0%}`      |

### `r`aw or `r`egex strings

-   raw string to ignore
    -   JS has [String.raw](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/raw)
-   [see the readable regex section](#readable-regex)

#### `r`egex strings

### Template strings

-   less powerful than `f` strings
-   useful for (malicious) user input

```python
from string import Template
templ_string = 'Hey $name, there is a $error error!'
Template(templ_string)
    .substitute(
        name=name,
        error=hex(errno))
```

### Nicer multi-line strings

```python
from textwrap import dedent

def copyright():
    print(dedent("""
        Copyright (c) 2022
        All Rights Reserved.
    """).strip("\n"))
```

## [Title case](https://www.pythonmorsels.com/title-case-in-python/)

### Avoid `"str".title()` alone

```python
>>> "don't".title()
"Don'T"
```

Use a regex

```python
import re

def title(value: str) -> str:
    titled = value.title()

    # Lowercase the whole regular expression match group.
    lowercase_match = lambda match: match.group().lower()

    titled = re.sub(r"([a-z])'([A-Z])", lowercase_match, titled)  # Fix Don'T
    titled = re.sub(r"\d([A-Z])", lowercase_match, titled)  # Fix 1St and 2Nd
    return titled
```

Use a library like [`titlecase`](https://github.com/ppannuto/python-titlecase) if you want small words (like `is` and `a`) to be lower case


## `urllib.parse.quote`

escape characters to put stuff in the URL


[urllib.parse — Parse URLs into components](https://docs.python.org/dev/library/urllib.parse.html#urllib.parse.quote)

```python
>>> quote('/El Niño/')`
'/El%20Ni%C3%B1o/'
```

### `quote_plus`

- replaces spaces with `+`
- instead of `%20`



quote vs quote_plus
