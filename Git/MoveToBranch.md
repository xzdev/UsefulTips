- Move last commit to a different branch
```
git branch newbranch
git reset --hard HEAD~1 # Go back 1 commit. You *will* lose uncommitted work.*1
git checkout newbranch
```
