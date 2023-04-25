# [Git Submodules](https://www.atlassian.com/git/tutorials/git-submodule)

-   git repos in a git repo
-   for example: zprezto uses them?

1. Add a submodule `git submodule add <URL to a git repo>`
2. Pulling from a repo with submodules

```bash
git clone <main repo URL>   # won't get submodule contents
cd <main repo dir>
git submodule init          # (like a git fetch, doesn't merge into your
git submodule update        # like git pull for the submodule

# or you could cd into the submodule and run
git pull
```

### When to use git submodules

1. private repo in public repo (like this notes repo!)
