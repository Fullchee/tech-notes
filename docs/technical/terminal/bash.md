# Bash

## https://jvns.ca/blog/2022/04/12/a-list-of-new-ish--command-line-tools/

-   https://explainshell.com/
-   [`tldr`](https://tldr.sh/)



## General Tips

### Double Dash (`--`)

-   tells shell to treat any future dashes like strings and not flags
    -   `npm test -- -u -t="ColorPicker"`
    -   the `-u` is a flag for the command and not `npm`
-

```bash
grep "--hello" data.txt
grep: unrecognized option '--hello'
```

```bash
grep -- --hello data.txt
```

#### Why `git checkout -- file.txt`

-   the `--` is optional in this case
-   just a good habit, since branches usually have dashes

### Command substitution

```bash
result=$(curl -X GET 'URL')
```

????

### String substitution

```bash
${var}

"$var_name"
```

????

-   TODO: what's the difference?



## Loops

### Looping over array

```bash
for var in "$@"
do
    echo "$var"
done
```
