### `-m` flag: Module

`python -m module_name args`

-   run a `m`odule
-   `python -m http.server`
    -   start http server on port 8000 in current directory
-   `python -m pdb path/to/file.py`
    -   debug a Python script
-   `python -m pip install ...`
    -   guarantee that you're running the version of `pip` that's connected to the current `python`

### `-i` flag: Interactive

Debug the state of a broken Python code when it crashed!

Although you should use `breakpoint()` and `pdb`

```python
$ python3 -i add.py 4 7
Traceback (most recent call last):
  File "/home/trey/add.py", line 5, in <module>
    print(sum(numbers))
TypeError: unsupported operand type(s) for +: 'int' and 'str'

# can debug to see the state of the program when it crashed!
>>> __name__
'__main__'
>>> sys.argv
['add.py', '4', '7']
>>> numbers
['4', '7']
```
