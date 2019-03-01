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

***
![](https://i.loli.net/2019/03/01/5c7887087635e.png)
* [git提交到远程藏库冲突解决](https://blog.csdn.net/gddxz_zhouhao/article/details/53070317)

*原因*
两人同时fetch了一个分支。 第一个人修改后提交，第二个人提交就失败。

*解决方法*
1.强制推送
$ `git push -f` 
可以提交，会将remote上第一个人的改动冲掉，比较暴力，不太好。
2.正常解决
先 `git fetch origin` 然后`git merge origin/master`, 和本地分支合并, 之后再`push`。  

* [GIT 的ORIGIN和MASTER分析](https://www.cnblogs.com/MarkTang/p/5759554.html)  

> 首先要明确一点，对git的操作是围绕3个大的步骤来展开的（其实几乎所有的SCM都是这样）
>
> 1. 从git取数据（git clone）
>
> 2. 改动代码
>
> 3. 将改动传回git（git push）
>
> 这3个步骤又涉及到两个repository，一个是remote repository，再远程服务器上，一个是local repository，再自己工作区上。其中
>
> 1, 3两个步骤涉及到remote server/remote repository/remote branch，
>
> 2涉及到local repository/local branch。git clone 会根据你指定的remote server/repository/branch，拷贝一个副本到你本地，再git push之前，你对所有文件的改动都是在你自己本地的local repository来做的，你的改动(local branch)和remote branch是独立（并行）的。Gitk显示的就是local repository。
>
>  
>
> 在clone完成之后，**Git 会自动为你将此远程仓库命名为origin（origin只相当于一个别名，运行git remote –v或者查看.git/config可以看到origin的含义）**，并下载其中所有的数据，建立一个指向它的master 分支的指针，我们用(远程仓库名)/(分支名) 这样的形式表示远程分支，所以origin/master指向的是一个remote branch（从那个branch我们clone数据到本地），但你无法在本地更改其数据。
>
> 同时，Git 会建立一个属于你自己的本地master 分支，它指向的是你刚刚从remote server传到你本地的副本。随着你不断的改动文件，git add, git commit，master的指向会自动移动，你也可以通过merge（fast forward）来移动master的指向。
>
>  $git branch -a (to show all the branches git knows about)
>
> \* master
>
>   remotes/origin/HEAD -> origin/master
>
>   remotes/origin/master
>
>  
>
> $git branch -r (to show remote branches git knows about)
>
>   origin/HEAD -> origin/master
>
>   origin/master
>
>  
>
> 可以发现，**master就是local branch，origin/master是remote branch（master is a branch in the local repository. remotes/origin/master is a branch named master on the remote named origin）**
>
> $git diff origin/master master （show me the changes between the remote master branch and my master branch).
>
> 需要注意的是，**remotes/origin/master和origin/master的指向是相同的**
>
> $git diff origin/master remotes/origin/master
>
>  
>
> git push origin master
>
> origin指定了你要push到哪个remote
>
> master其实是一个“refspec”，正常的“refspec”的形式为”+<src>:<dst>”，冒号前表示local branch的名字，冒号后表示remote repository下 branch的名字。注意，如果你省略了<dst>，git就认为你想push到remote repository下和local branch相同名字的branch。听起来有点拗口，再解释下，push是怎么个push法，就是把本地branch指向的commit push到remote repository下的branch，比如
>
> $git push origin master:master (在local repository中找到名字为master的branch，使用它去更新remote repository下名字为master的branch，如果remote repository下不存在名字是master的branch，那么新建一个)
>
> $git push origin master （省略了<dst>，等价于“git push origin master:master”）
>
> $git push origin master:refs/for/mybranch (在local repository中找到名字为master的branch，用他去更新remote repository下面名字为mybranch的branch)
>
> $git push origin HEAD:refs/for/mybranch （HEAD指向当前工作的branch，master不一定指向当前工作的branch，所以我觉得用HEAD还比master好些）
>
> $git push origin :mybranch （再origin repository里面查找mybranch，删除它。用一个空的去更新它，就相当于删除了）

## Reference  
- [Git教程](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)  
- [Git Cheat Sheet](http://www.cheat-sheets.org/saved-copy/git-cheat-sheet.pdf)
- [常用 Git 命令清单](http://www.ruanyifeng.com/blog/2015/12/git-cheat-sheet.html)