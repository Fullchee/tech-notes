# Regex

[re — Python docs](https://docs.python.org/3/library/re.html)

## [`re.match` vs `re.search`](https://stackoverflow.com/a/180993/8479344)

-   `match` at the beginning of the string, or `match` the entire string
    -   faster
-   Otherwise use search
-   both return a [re.Match object](https://docs.python.org/3/library/re.html#match-objects)

```python
>>> m = re.match(r"(.*)BC(.*)", 'ABC-DE')
>>> m.group(2)
'-DE'
```

### Always use `r`aw (`r`egex) strings

-   so that it doesn't escape `"C:\Programs\nathan"`
-   `\n` is a newline 😱
-   `r"C:\Programs\nathan"`
    -   is what we expect 😄
-   need to escape `^` and `$` and other chars though 😞

```python
# need to escape $
>>> re.search(r"$100", "$100") == None
True
>>> re.search(r"\$100", "$100")
<re.Match object; span=(0, 4), match='$100'>
```

## [Readable Regex](https://www.youtube.com/watch?v=0sOfhhduqks)

### Why regex is hard?

Every character is a statement

Like trying to write/read minified JS

### [Verbose mode](https://youtu.be/0sOfhhduqks?t=3868)

Min 64 (t=3868)

you can leave comments too!

```python
def is_valid_uuid(uuid: str) -> bool:
    return bool(re.match(r"""
        ^
        [a-f\d]{8}  # 8 hex digits
        -
        [a-f\d]{4}  # 4 hex digits
        -
        [a-f\d]{4}  # 4 hex digits
        -
        [a-f\d]{4}  # 4 hex digits
        -
        [a-f\d]{12} # 12 hex digits
        $
    """, uuid, re.IGNORECASE | re.VERBOSE))
```

### Using f-strings & r-strings with regex

https://death.andgravity.com/f-re
