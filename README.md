# Git commands
## Git stash only unstaged changes
```
git add <files><to> <stage>
git stash push --keep-index
```
## Git revert commit before push
```
git reset HEAD~1
```
## Git reset branch to master
```
git reset --hard origin/master
git push -f
```
