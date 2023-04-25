fd

## list of files with name only (no path)

```bash
fd . -X printf '%s\n' {/}
```

```bash
find ./dir1 -type f -exec basename {} \;
```