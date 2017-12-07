---
title: Linux Command
date: 2017-12-05 14:22:02
categories: Linux
tags: [Linux, command, shell]
---

We have below users and their password:
- root
- ryan (sudoer)
- grace
 
## User & Password ##
Login as ryan:

- check password expiration
```bash
chage -1 ryan	# number 1
```
<!--more-->
- change password
```bash
passwd			# for user self
```
- login as `root`
```bash
su - root
```
- change password for `grace`
```bash
passwd grace
```
- login as `grace`
```bash
su grace
```
- become `root`
```bash
sudo su - root
```
- set password never expire, must done by root
```bash
chage ryan
	
	Minimum password age:0
	Maximum password age:99999
	Last password change: enter
	Expiration warning: enter
	Password Inactive: enter
	Account expiration date: -1
```

## File & Directory ##

- check directory size
```bash
du -sh <path>
```
- monitor log
```bash
tail -100f <file>
```
- monitor log and catch specific content
```bash
tail -100f <file> | grep "<content>"
```




