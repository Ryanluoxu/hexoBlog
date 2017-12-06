---
title: 'Git - 学习笔记'
date: 2017-11-24 22:46:23
categories: Git
tags: [Git, 学习笔记]
---

**声明：本文为 ryanluoxu 原创文章，欢迎转载，请在明显位置注明出处。**

学习素材：[Pro Git](https://bingohuang.gitbooks.io/progit2/content/02-git-basics/sections/getting-a-repository.html)

# 常用指令 #

```bash
git add		#添加到下一次的提交中。
git status -s	#状态简览
git diff --staged	##暂存区域 - 本地 Repo
git commit -a -m 'comment'	#跳过git add
```

Git 周期
![Git 周期](/images/Git 周期.png)

<!--more-->

# Git 基础 #

## 获取 Git 仓库 ##

两种方法：

1. 初始现有文件夹    
```
git init
```
	初始后的文件夹里多了一个 .git 的文件夹，这就是本地 repository。
2. 克隆已有的 Remote Repository
```
git clone https://github.com/Ryanluoxu/learn_linux.git
```
	会在当前文件夹里生成 `learn_linux` 文件夹。里面也有 .git 文件夹作为本地 repository。 Remote repository 里的内容先进入到本地 repository，然后才到 `learn_linux` 文件夹。

## 提交文件 ##
### 文件的三种状态 ###
- 已修改 modified ： 对某个文件进行修改，保存完成。
- 已暂存 staged ： 执行 `git add` 之后
- 已提交 committed ： 执行 `git commit` 之后

这里的提交目的地，是本地 repository。  
常用的 github 为 remote repository。   
如果需要将本地 repository 同步到 github 上，需要执行 `git push`。    

所以对本地文件进行修改，到同步到 github，基本流程如下：   
  
![本地修改-github的流程图](/images/本地修改-github的流程图.jpg)


### git status ###
```
git status
git status -s	#状态简览
```
举例：
```bash
 M README			#文件被修改了但是还没放入暂存区
MM Rakefile			#文件被修改，放入了暂存区之后。该文件又被修改。
A  lib				#新添加到暂存区中的文件
M  simple.txt		#文件被修改了并放入了暂存区
?? LICENSE.txt		#新添加的未跟踪文件
```


### git ignore ###
创建一个名为 `.gitignore` 的文件，列出要忽略的文件模式。
```bash
# no .a files
*.a

# but do track lib.a, even though you're ignoring .a files above
!lib.a

# only ignore the TODO file in the current directory, not subdir/TODO
/TODO

# ignore all files in the build/ directory
build/

# ignore doc/notes.txt, but not doc/server/arch.txt
doc/*.txt

# ignore all .pdf files in the doc/ directory
doc/**/*.pdf
```

### git diff ###

```bash
git diff			#本地文件 - 暂存区域
git diff --staged	#暂存区域 - 本地 Repo
```

### git commit ###
```bash
git commit -m "Story 182: Fix benchmarks for speed"
```

跳过 `git add`， 把所有跟踪下的文件暂存，然后提交。
```bash
git commit -a -m 'added new benchmarks'
```


## 远程仓库 ##

查看已经配置的远程仓库服务器:
```
git remote -v
```

添加远程 Git 仓库:
```
git remote add <shortname> <url>
```

抓取：从远程仓库中获得数据,放到本地仓库：
```
git fetch [remote-name]
```

拉取：从远程仓库中获得数据，然后合并到当前分支：
```
git pull
```

### Push existing project to github ###

1. Create new repo in github called : hexoBlog
2. git bash
```bash
$ git init
$ git add --all
$ git commit
$ git remote add origin https://github.com/Ryanluoxu/hexoBlog.git
$ git push
$ git status
```
4. there is one folder always in `untracked` mode. 
```
modified:   next (modified content, untracked content)
```
5. realised `next` is cloned from github. Itself contains a .git folder.
6. remove `next` local git repo.
```bash
$ cd theme/next/
$ rm -rf .git
$ cd ../..
$ git status

nothing to commit, working tree clean

$ git push

fatal: The current branch master has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin master


$ git push -u origin master		#org

```
