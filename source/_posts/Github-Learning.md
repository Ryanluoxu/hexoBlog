---
title: Github Learning
date: 2017-12-07 14:45:54
categories: Git
tags: [github, git, notes]
---

## Switching remote URLs between SSH and HTTPS
Check existing remote:
- If SSH:
```bash
$ git remote -v
origin  git@github.com:USERNAME/REPOSITORY.git (fetch)
origin  git@github.com:USERNAME/REPOSITORY.git (push)
```
- If HTTPS:
```bash
$ git remote -v
origin  https://github.com/USERNAME/REPOSITORY.git (fetch)
origin  https://github.com/USERNAME/REPOSITORY.git (push)
```
<!--more-->
Change your remote's URL from SSH to HTTPS
```bash
$ git remote set-url origin https://github.com/USERNAME/REPOSITORY.git
```
Change your remote's URL from HTTPS to SSH 
```bash
$ git remote set-url origin git@github.com:USERNAME/REPOSITORY.git
```
Reference: https://help.github.com/articles/changing-a-remote-s-url/

## git push without entering username & password

### HTTPS
For the repo which is cloned from GitHub using HTTPS, use a credential helper to remember username and password.

With Git for Windows, run the following commands to store credentials:
```bash
git config --global credential.helper wincred
```

### SSH
For the repo which is cloned from GitHub using SSH, use SSH keys. -> [Generating an SSH Key](https://help.github.com/articles/generating-an-ssh-key)

Reference:[Caching your GitHub password in Git](https://help.github.com/articles/caching-your-github-password-in-git/#platform-windows)