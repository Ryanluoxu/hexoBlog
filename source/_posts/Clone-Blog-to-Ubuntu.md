---
title: Clone Blog to Ubuntu
date: 2017-12-07 12:21:12
categories: 搭建博客
tags: [blog, hexo, ubuntu, migrate]
---

My current working space for this hexo blog is in windows 10.

This is how I migrate to Ubuntu.

# upload project to github
1. create new repo in github called : hexoBlog
2. open git bash on blog folder, and run:
```bash
$ git init
$ git add --all
$ git commit
$ git remote add origin https://github.com/Ryanluoxu/hexoBlog.git
$ git push
```
3. If any folders inside are cloned from github. Need to remove .git first:
```
$ rm -rf .git
```
4. `git push` may face "fatal: The current branch master has no upstream branch". Run:
```
$ git push -u origin master
```

Now project is on the github.

# clone project to Ubuntu

```bash
$ git push -u origin master	#1 install git
$ mkdir ~/git			#2 create folder git under home
$ cd ~/git
$ git clone https://github.com/Ryanluoxu/hexoBlog.git	#3 clone project from github
```

Now local working space is : ~/git/hexoblog/
 

# installation

```bash
$ curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.2/install.sh | bash	#1 install Node Version Manager
$ nvm install stable	#2 install Node.js
$ npm install -g hexo-cli	#3 install hexo
```


# Hexo setup

```bash
$ hexo init ~/git/hexoBlog
$
```

$ npm install hexo --save


## Install ##

- install git
```
$ sudo apt install git
```
- install nodejs
```
$ sudo apt-get update
$ sudo apt-get install nodejs	
$ sudo apt-get install npm	# package manager
```

