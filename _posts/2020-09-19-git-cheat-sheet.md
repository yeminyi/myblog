---
layout: post
title: Git Cheat Sheet
categories: git
tags: [git]
---

## GIT Basic

git log    
Display the entire commit history using the default format.For customization see additional options<br>
git log -[limit] <br>
Limit number of commits by [limit]. <br>
E.g. ”git log -5” will limit to 5 commits. <br>
git log --follow [file]<br>
Lists version history for a file, including renames

git diff    <br>
Show unstaged changes between your index and working directory.<br>
git diff HEAD <br>
Show difference between working directory and last commit.<br>
git diff --cached <br>
Show difference between staged changes and last commit<br>
git diff [first-branch]...[second-branch]<br>
Shows content differences between two branches

git show [commit] <br>
Outputs metadata and content changes of the specified commit

## Deleting Branches

Deleting local branches

```
git branch -a
# *master
#  test
#  remote/origin/master
#  remote/origin/test

git branch -d test
# Deleted branch test .

```

Deleting remote branches

```
git branch -a
# *master
#  test
#  remote/origin/master
#  remote/origin/test

git push origin --delete test
# To <URL of your repository>.git
#  - [deleted]         test

```
## Github First Commit
```
git init
git add .
git commit -m "first commit"
git branch -M master
git remote add origin https://github.com/yourusername/repo.git
git push -u origin master
```
## Git Hard Reset
1. find the commit id using `git log`
   
       eg :id is fae696654853ae76cfa7f38a461c438cf75ba965

2. reset the old one
    
    ```
    git reset --hard fae696654853ae76cfa7f38a461c438cf75ba965
        
    ```
3. push it to remote server
   
    ```
    git push -f -u origin master  
    ```
_____________________________________________________________
    ```

    git reset --soft HEAD^      (going back to soft, not back to cancel the `git add`,the code is still changed)

    git reset --hard HEAD       (going back to HEAD)

    git reset --hard HEAD^      (going back to the commit before HEAD)

    git reset --hard HEAD~2     (going back two commits before HEAD)

    ```

## Changing a remote's URL

    List your existing remotes in order to get the name of the remote you want to change.
    ```
    git remote -v
    > origin  git@github.com:USERNAME/REPOSITORY.git (fetch)
    > origin  git@github.com:USERNAME/REPOSITORY.git (push)
    ```

    Change your remote's URL from SSH to HTTPS with the git remote set-url command.
    ```
    git remote set-url origin https://github.com/USERNAME/REPOSITORY.git
    ```