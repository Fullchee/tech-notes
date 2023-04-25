# Natural Sort

Anthony Writes Code

you can split a string with a regex!

```python
num_splitter = re.compile('([0-9]+)')
```

```python
num = re.compile('([0-9]+)')

def natural_key(s: str) -> List[str | int]:
	return [
		int(part)
		if part.isdigit()
		else part
		for part in num_splitter.split(s)
	]

# edge case: '0300' and '300' will have the same key
# break ties by comparing the original strings
list.sort(key=lambda s: (natural_key(s), s))

# case insensitive
list.sort(key=lambda s: (natural_key(s.lower()), s.lower(), s))
```
