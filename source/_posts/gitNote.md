---
title: gitNote
date: 2018-09-23 00:42:34
author: SmalBox
img: /images/pageHeadImg/git.png
tags:
  - git
  - note
---
# Git command note

## Install: initialize user name and user email.

``` bash
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```

## 1.Create git

``` bash
$ mkdir learnBox //创建目录作为仓库
$ cd learnBox //进入目录
$ pwd //显示仓库位置
$ git init //创建仓库（仓库根目录下有.git的隐藏目录，用ls -ah可以看到）
```

## 2.Add & Commit file

``` bash
$ git add readme.txt //添加文件到仓库
$ git commit -m "add readme.txt" //提交以上添加，填写修改信息
```

## 3.Check the status & difference

``` bash
$ git status //查看仓库状态
$ git diff readme.txt //查看具体修改了哪些
$ git log //从近到远查看提交日志
$ git log --pretty=oneline //简化日志每个只显示一行
```

## 4.Reset

``` bash
$ git reset --hard HEAD^ //退回上一个版本 '^'退回一个 '~100'退100个
$ git reset --hard <version id> //版本号写前几位即可，git自己会找
$ git reflog //记录执行过的命令
```

## 5.Stage(index)

``` bash
使用 "git add" 命令将工作区文件添加到stage暂存区。
使用 "git commit" 命令将stage暂存区中文件添加到分支。
```
## 6.Manage modify

``` bash
先add添加到stage，后commit到分支。
$ git diff HEAD -- readme.txt //查看工作区和版本库中最新版本区别
```

## 7.Undo changes

``` bash
1)无add无commit：
	$ git checkout -- <file>
2)有add无commit：
	$ git reset HEAD <file>
	$ git checkout -- <file>
3)有add有commit：
	$ git reset --hard HEAD^//退回上一版本
```
	
## 8.Remove file

``` bash
$ rm <file> //删除工作区的文件
$ git rm <file> //如果真的想删，删除版本库里的文件
$ git checkout -- <file> //误删了工作区文件，用版本库恢复删除文件
```


## Remote repository

``` bash
$ ssh-keygen -t rsa -C "email@example.com" //创建ssh协议公钥和私钥
//进入到GitHub中添加ssh key 即可远程推送
```

## 9.Add and remove remote repository =

``` bash
$ git remote add origin https://github.com/SmalBox/learngit.git
$ git remote add origin git@github.com:SmalBox/learngit.git
//GitHub上的提示添加远程库.这两种都可以
$ git remote rm <remote name> //移除远程库
$ git push -u origin master //将本地库推送到GitHub
```

## 10.Clone from remote repository

``` bash
$ git clone git@github.com:SmalBox/repositoryName.git //从远程克隆到本地
```

## Manage branch

## 11.Create & Combine branch

``` bash
$ git branch //查看分支结构
$ git branch <name> //创建分支
$ git checkout <name> //切换分支
$ git checkout -b <name> //创建并切换分支
$ git merge <name> //合并某分支到当前分支
$ git branch -d <name> //删除某分支
$ git branch -D <name> //强行删除某分支，例如强行删除未合并的分支
```

``` bash
$ git checkout -b dev //创建并切换 到dev分支
$ git branch //查看 分支
$ git checkout master //切换 到master分支
$ git merge dev //把dev分支 合并 到master分支
$ git branch -d dev //删除 dev分支
```

## 12.Conflict fixed

``` bash
//当两个分支修改同一个文件，合并时产生冲突。
//在当前分支修改冲突文件，再add和commit之后重新合并。
$ git log --graph --pretty=oneline --addrev-commit //查看分之合并图
```
	
## 13.Branch strategy

``` bash
$ git merge --no-ff -m "merge with no-ff" dev //不使用Fast
forward合并，创建一个commit记录。
```

## 14.Bug branch(Stach)

``` bash
$ git stash //把暂时没完成的分支储藏起来
$ git stash list //列出存储的各个版本
$ git stash pop //恢复储藏，并删除stach记录
$ git stash apply stash@{0} //恢复到stash0
$ git stash drop //删除stash内容
```

## 15.Collaboration

``` bash
$ git remote //查看远程仓库信息(name)
$ git remote -v //查看远程仓库详细信息
$ git push <git name> <branch name> //推送分支 例如：git push origin master
$ git checkout -b dev origin/dev //创建本地dev链接远程仓库中的dev
$ git pull //推送失败，远程分支新，用此试图合并
$ git git  branch --set-upstream-to=<remote name>/<branch name> //无跟踪信息时，说明本地分支与远程分支没有建立关系，用此建立
```

## 16.Tag

``` bash
$ git tag <name> //给当前分支打标签,标签打在最新提交的commit上
$ git tag //查看当前分支的标签
$ git tag <name> <commit id> //给某一个版本的commit打标签
$ git tag -a <tag name> -m "description" <commit id> //带有说明的标签
$ git tag -s <tag name> -m "description" <commit id> //私钥签名一个标签
$ git show <tag name> //查看标签信息
$ git tag -d <tag name> //删除标签
$ git push <remote name> <tag name> //推送某一标签到远程仓库
$ git push <remote name> --tags //推送全部标签到远程
//删除远程标签，要先删除本地标签，再推送远程。格式如下：
$ git tag -d <tag name> //删除本地标签
$ git push <remote name> :refs/tags/<tag name> //推送远程
```

## 17.Alias

``` bash
$ git config --global alias.co checkout //设置全局简写
$ git config --global alias.st status 
$ git config --global alias.ci commit
$ git config --global alias.br branch
$ git config --global alias.lol "log --pretty=oneline"
$ git config --global alias.glol "log --graph --pretty=oneline --abbrev-commit"
//全局的配置文件在用户目录下名为：.gitconfig中记录。每个仓库的配置文件在仓库下的.git文件下config文件中记录
```