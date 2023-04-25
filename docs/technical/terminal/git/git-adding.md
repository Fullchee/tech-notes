# Git adding

## Make an existing file executable

```bash
git add --chmod=+x -- afile
```

## Run a git command in another directory

`git -c <directory> <git_command>`

## Sparse Checkout

### Why sparse checkout

????

### How to sparse checkout

```bash
mkdir <repo>
cd <repo>
git init
git remote add -f origin <url>
git config core.sparseCheckout true
```

-   If you only want to ignore a single file without adding to the `.gitignore`, add the same structure to the `.git/info/exclude`, same structure as `.gitignore`
