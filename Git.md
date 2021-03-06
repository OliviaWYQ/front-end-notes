# Git notes

## change the last commit
```
git commit --amend
```
=
```
git add .
git commit -m "x"
git log --oneline -5
git rebase -i xxx
squash
wq
```

## track remote branch
```
git branch -a
```
```
  master
  remotes/origin/HEAD -> origin/master
  remotes/origin/dev
  remotes/origin/master
```
  
To create a local branch dev from remotes/origin/dev:
```
git fetch origin dev:dev
```
then you see:
```
  dev
  master
  remotes/origin/HEAD -> origin/master
  remotes/origin/dev
  remotes/origin/master
```

```
git checkout dev
git branch --set-upstream-to=origin/dev 
```
it will track the content from the remote branch

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

## When you rebase but face conflict
open Visual Studio Code, and edit the file
```
git add .
git rebase --continue
```

## When files loss, use reflog to see the history

```
git reflog
git checkout -b recovery <commit-id>
```

## Revert CR

Go to the link and find out commit id, eg. https://code.amazon.com/packages/AxleAppReactNative/commits/76013ae5670f73e23975ae83e653718622610a29#
```
cd AxleAppReactNative
git pull
git revert 76013ae5670f73e23975ae83e653718622610a29
git add .
git revert --continue
cr
```

## Git reset 

$ git reset HEAD^            # 回退所有内容到上一个版本  
$ git reset HEAD^ hello.php  # 回退 hello.php 文件的版本到上一个版本  
$ git  reset  052e           # 回退到指定版本
