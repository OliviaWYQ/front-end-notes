# Git notes

## Pull the latest code from the server
```
git checkout mainline
git pull
```

## Update the code and squash
```
git log --oneline -5
git rebase -i <commit-id-you-want-to-rebase>
```
inside vim, for the second commit, change 'pick' to 'squash'
```
:wq
```
inside vim, change the commit message
```
:wq
```
Now you can see 2 commits squash into one

## Change the commit message for the latest commit
```
git commit --amend -m "your message"
```

## Rename branch
```
git branch -m old-name new-name
```
