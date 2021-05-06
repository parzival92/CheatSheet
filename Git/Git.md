# Git Concepts


```
#Git log shows list of file changed
git log --name-only

#Git log show last 3 commit 
git log -n 3

#Create new branch
git branch <branchname>

#Switch to Existing Branch
git checkout <branchname>

#Create new branch and switch to it
git checkout -b <branchname>

#Delete a branch
git branch -d <branchname>

#List all branches
git branch

#List local and remote branches
git branch -a
```

### Git Merge

```
git checkout <branchname>
git merge <targetbranch>

```

### Remote Repositories

```
git remote add origin <repo-url>

git clone <sshurl>

#When changes are on remote not on local
git fetch origin master
git merge origin master

#git pull (git fetch and git merge)
git pull origin master

```

### Cherry Pick


```
#Get Particular commit in your working area
git cherry-pick 7d6f462

```

### Resetting and Reverting

```
git revert HEAD~0

git reset --soft Head~3
```

### Stashing

```

git stash
git stash list
git stash pop 
git stash show stash@{1}

git reflog
```




