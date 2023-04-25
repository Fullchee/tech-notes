# Terminal files

## Reading files

### [bat](https://github.com/sharkdp/bat)

-   `cat` + `less` + `git` + more

#### `less`

-   `-N`show line numbers
    -   has syntax highlighting

## Editing Files

#### [Delete lines that match pattern](https://stackoverflow.com/a/5410784/8479344)

-   Delete lines that match
    -   Used in [[work-aws]]

```bash
sed -i '' '/^\[localhost\]:56789/d' ~/.ssh/known_hosts;
```

### How to append to a protected file (with sudo)

```bash
echo '127.0.0.1 redirected-url.com' | sudo tee -a /etc/hosts
```

-   [tee](https://www.gnu.org/software/coreutils/manual/html_node/tee-invocation.html#tee-invocation)
    -   read from standard input and write to standard output and files (or commands).

## Listening to files

### [Entr](https://github.com/eradman/entr)

Run arbitrary commands when files change
