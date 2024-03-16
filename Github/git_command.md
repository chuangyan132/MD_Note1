# Git Command
## Day1 
### Git confilct error
- local branch has diverged from the branch on the remote repository (origin/main in this case). This divergence means that there have been changes both in your local branch and in the remote branch that Git cannot automatically reconcile without further instructions.
- The error message suggests three possible ways to reconcile the divergent branches:
  - merge (the default strategy)
  - rebase
  - fast-forward only
```bash
error:
git pull --tags origin main
From https://github.com/chuangyan132/MD_Note1
 * branch            main       -> FETCH_HEAD
hint: You have divergent branches and need to specify how to reconcile them.
hint: You can do so by running one of the following commands sometime before
hint: your next pull:
hint: 
hint:   git config pull.rebase false  # merge (the default strategy)
hint:   git config pull.rebase true   # rebase
hint:   git config pull.ff only       # fast-forward only
hint: 
hint: You can replace "git config" with "git config --global" to set a default
hint: preference for all repositories. You can also pass --rebase, --no-rebase,
hint: or --ff-only on the command line to override the configured default per
hint: invocation.
fatal: Need to specify how to reconcile divergent branches.

```
```bash
#1, Merge Default Strategy
git pull --tags origin main --no-rebase

#2, Rebase Merge changes from the the remote branch into the current branch
git pull --tags origin main --rebase

#3, Fast-Forward Only reply local changes on top of the fetched branch
git pull --tags origin main --ff-only
```

