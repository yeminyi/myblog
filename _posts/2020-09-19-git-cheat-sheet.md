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
## Github first commit
```
git init
git add .
git commit -m "first commit"
git branch -M master
git remote add origin https://github.com/yourusername/repo.git
git push -u origin master
```