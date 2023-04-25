# Git

## Undoing

### Undo a `git rm` for a single file

-   terminal: `--` is often used
    -   any future dashes are considered strings and not flags
-   useful when the file path or branch name has dashes
    -   `git reset -- my-file.txt`
    -   `git reset my-file.txt`
        -   will think `-f` is a flag

```
undo-rm() {
	filePath="$1"
	git reset -- $1
	git checkout -- $1
}
```

(can't do a git alias because it's multiple lines)

### Undo all changes to a single file in a PR

```bash
git restore --source origin/main backendcore/dashboard_etl_manager/views
```

### Move a file from the 'staged' state to 'unstaged' state

`git reset HEAD <file>`

## git-stash

| Create a stash      | `git stash`     |
| ------------------- | --------------- |
| Pop the first stash | `git stash pop` |

|                                  |                                                     |
| -------------------------------- | --------------------------------------------------- |
| View stashes                     | `git stash list`                                    |
| Create a named stash             | `git stash -m "stash name"`                         |
| Save a stash with specific files | `git stash push -m stash_name -- file1 file2 file2` |

## git revert "hash"

-   git revert undoes only that provided hash's changes
-   it will still keep all the other commits' changes
-   **set the HEAD as a previous commit**: `git revert --no-commit 0766c053..HEAD`
    -   `--no-commit` lets you revert every commit without creating a new commit for each
    -   safe, no history change
-   git shows `(cherry-or-revert)`, use `git revert --quit`

### `git reset` vs `--hard`

-   staged -> unstaged: `git reset -- file`

#### `--hard`

-   move tip of branch (HEAD) to a different commit
    -   A -> B -> C = HEAD
    -   `git reset --hard A`
    -   B and C will be lost
    -   git reflog to recover the commits!
        -   (quickly! otherwise git might garbage collect)

![](https://i.stack.imgur.com/qRAte.jpg)

#### reset vs checkout on files

-   reset: staged snapshot matches the given commit
-   checkout: working file matches the given commit

## git diff

-   Just get files that changed `git diff --name-status <commit/branch1> <commit/branch2>`
