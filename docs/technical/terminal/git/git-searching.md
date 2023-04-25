# Searching Git History

## [`.git-blame-ignore-revs`](https://docs.github.com/en/repositories/working-with-files/using-files/viewing-a-file#ignore-commits-in-the-blame-view)

```bash title=".git-blame-ignore-revs"
# Removed semi-colons from the entire codebase
a8940f7fbddf7fad9d7d50014d4e8d46baf30592
# Converted all JavaScript to TypeScript
69d029cec8337c616552756310748c4a507bd75a
```

## Git Log / blame

-   View all commits that modified a file or a directory
-   `git log --follow <path_to_dir_or_file>`
    -   don't use `git log -p`, that shows the entire diff
-   Get the SHA of the latest commit that changed a file
    -   `git --no-pager log -n 1 --pretty=format:%H -- <path_to_file_or_dir>`

## Git searching history

### View how one file's changed across time

-   `git log --follow -p -- file`
-   Simpler version that doesn't follow: `git log -p <filename>`

### Git search across branches

```
git grep "DialChart" `git show-ref --heads`
```

**If that comes up empty**

```
git grep "DialChart" $(git rev-list --all)
```

## Git analytics

### View the number of commits each person made

```bash
git shortlog -sen
```

```bash
git shortlog -sen COMMIT_HASH..HEAD
```

-   `s`: summary
-   `n`: sorted by number of commits
-   `e`: email

### Get a commit from a specific time

```bash
git log --after="2022-03-01 00:00" --before="2022-03-01 23:59"
```
