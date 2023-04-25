## `breakpoint()`

-   https://www.youtube.com/watch?v=IzgSl-tkPPg
-   `n` next / step over
-   `s` step into
-   `l` list code
-   `j <line>` jump to line
-   `b <line>` or `break <line>` set breakpoint
-   `c` or `continue` until breakpoint
-   `h` help

or start a file with PDB

```bash
python -m pdb file.py
```

## `pudb`

Visual `pdb`

useful for debugging in a container
- when an IDE debugger might get out of sync

1. `pip install pudb`
2. `import pudb; pu.db`
	1. in the source code
	2. instead of `breakpoint()`