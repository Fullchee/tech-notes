# Git stuff that's ingrained in my head

## Locally ignoring

```
git update-index --skip-worktree [<file>...]         (create a git alias <git ignore>)
git update-index --no-assume-unchanged [<file>...]   (create a git alias <git unignore>)
```

## Make the local repo exactly like remote

```bash
git reset --hard origin/main
```

-   won't touch unstaged files files
-   may be able to recover unpushed commits via git reflog
