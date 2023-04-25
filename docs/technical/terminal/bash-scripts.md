# Bash scripts

## Tools

### [ShellCheck](https://www.shellcheck.net/)

-   linter for Bash
-   [VSCode ShellCheck extension](https://marketplace.visualstudio.com/items?itemName=timonwong.shellcheck)

### Bash boilerplates

-   [Minimal boilerplate](https://betterdev.blog/minimal-safe-bash-script-template/)
    -   ~80 lines
-   [b3bp](https://bash3boilerplate.sh/)
    -   ~500 lines

### `set`

set or unset values

```bash

#

# Do
set -o nounset
# Catch the error in case mysqldump fails (but gzip succeeds) in `mysqldump |gzip`
set -o pipefail
# Turn on traces, useful while debugging but commented out by default
# set -o xtrace
```

|      |                                                              |
| ---- | ------------------------------------------------------------ |
| `-e` | - Exit immediately if a command exits with a non-zero status |

|
| `-o <option_name>` | `--option-name` |
| `-o errexit` | - exit on error

-   Append `"|| true"` if you expect an error |
    | `-o errtrace` | - Exit on error inside any functions or sub-shells |
    | `-o nounset` | - no undefined vars
-   Use `${VAR:-}` to use an undefined var |
    | `-u` | reference a variable that hasn’t been previously defined? throw an error |
    | `-x` | all executed commands are printed to the terminal |
-   `cmd1 | cmd2 | cmd3`
-   if any of the commands fail, exit with an error
-   pipeline to return the exit status of the last (rightmost) command to exit with a non-zero status
-

[See bash page for more bash goodies](./bash)
