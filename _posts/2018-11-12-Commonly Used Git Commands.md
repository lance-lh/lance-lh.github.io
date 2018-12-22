---
layout:     post
title:      Commonly Used Git Commands
#subtitle:   None
date:       2018-11-12
author:     Lance
header-img: img/bg.jpg
catalog: true
tags:
    Git
---

## Content  

![](https://i.loli.net/2018/12/22/5c1de5e71e490.png)

### Enter the local directory first
```shell
cd directory
```
### Initialize the folder
```shell
git init
```
### Add files to staging area
```shell
git add <file>
git add -all
```
### Add files to repository
```shell
git commit -m <message>
```
### Show file status of working directory
```shell
git status
```
### Show modified content of file in working directory
```shell
git diff <file>
```
### Show history
```shell
git log
```
### Change version
```shell
git reset --hard commit_id
git reset --hard HEAD^
git reset --hard HEAD^^
```
### Watch command history
```shell
git reflog
```
### Discard changes in working directory
```shell
git checkout --file
```
### Remove files from the working tree and from the index
```shell
1.
git rm test.txt
git commit -m "delete test.txt"
git push  
2. 
rm test.txt
git commit -am "delete test.txt"
git push  
3.
git rm folder -r -f 
git commit -m "delete folder"
git push  
```
### Connecting to Github
```shell
git remote add origin git@github.com:username/repository_name.git
git push -u origin master
git push origin master
```

### Branch operation
```shell
git branch
git checkout -b dev
git checkout master
git merge dev  # merge dev branch into current branch
git branch -d dev
```
### Overwrite local repo
```shell
git fetch --all # download remote repo
git reset --hard origin/master # HEAD points to the newest version
```

## Reference  
- [Git教程](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)  
- [Git Cheat Sheet](http://www.cheat-sheets.org/saved-copy/git-cheat-sheet.pdf)