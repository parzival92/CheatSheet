# Git Concepts

```
git commit -a -m "Add a heading to index.html"
```
The -a option adds all of the files you modified since the last commit. It won't add new files. For that, you still need git add.

```
git diff
git diff head
```
The default is for git diff to compare the working tree to the index. In other words, it shows you all of the changes that haven't been staged (added to the index) yet. To compare the working tree to the last commit, you can use git diff HEAD.

* **Git doesn't consider adding an empty directory to be a change. That's because Git only tracks changes to files, not directories.**

```
git log --oneline
```

#### How to recover deleted file


Remove file
```
rm index.html
```
Recover with checkout
```
git checkout -- index.html
```
If we remove with git rm
```
git rm index.html
```
then try git checkout it will give error as it as removed index also solution is to use git reset
```
git reset HEAD index.html
```
Above is scenario where you are on working tree and nothing has committed now how to handle recovery when changes are committed
```
git revert --no-edit HEAD
git checkout -- index.html
```
The --no-edit flag here tells Git that we don't want to add a commit message for this action.


