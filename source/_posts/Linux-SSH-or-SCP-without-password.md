---
title: Linux - SSH or SCP without password
date: 2017-11-28 23:24:20
categories: Linux
tags: [Linux, SSH, SCP, password, server]
---

**声明：本文为 ryanluoxu 原创文章，欢迎转载，请在明显位置注明出处。**

点这里跳过废话：[直奔主题 Show me the code](#直奔主题)

有这样一个任务: 将同事发送的原始数据处理好之后，放进数据库。
其中一个关键的步骤，就是原始数据的转移。

通常我们有两个服务器，一个是 Public_Server，一个是 Private_Server。 
公开 Public_Server 的用户名和密码，这样其他同事都可以自由地往里面存放数据。
然后我们操作 Private_Server 来获取那些数据，再进一步处理。

> 好处：
> - 保护处理数据的程序和数据库
> - 有时需要换服务器，避免通知所有人更新服务器的地址和登录信息
> - Public_Server 就像一个保护屏，做了一个分割，提高了安全性。

<!--more-->
转移数据，作为整个工序里很小的一个步骤，通常我们会直接写进一个脚本里，这部分都会自动完成。
但是在服务器之间做这个操作，会需要提供密码，此时，整个脚本程序就会停下来。如果需要人来输入密码，就失去了脚本的意义了。
所以事先在两个服务器之间建立信任，这样，需要 SCP 或者 SSH 的时候，都不需要再输入密码。

<a name="直奔主题"/>
**具体操作如下：**

假设：

- Public_Server: 
```
IP： 199.99.999.99
UserId: people 
```
- Private_Server:
```
UserId: ryan
```

在 Private_Server 上操作：

1. 创建钥匙。
```bash
ssh-keygen -t rsa
```
	一路回车之后，做了两个钥匙。自己的钥匙是这个：
```bash
/home/ryan/.ssh/id_rsa
```
	公开的钥匙是这个：
```bash
/home/ryan/.ssh/id_rsa.pub
```
2. SSH 连接到 Public_Server, 并且创建 .ssh 文件夹
```bash
ssh people@199.99.999.99	# 输入密码，进入到 public server
cd ~					# 进入 people 用户的 Home
mkdir .ssh				# 创建 .ssh 文件夹(/home/people/.ssh)
exit					# 退出，回到 private server
```
3. 将公开的钥匙复制到 public server 的 .ssh 文件夹里，命名为 authorized_keys，需要密码
```bash
scp /home/ryan/.ssh/id_rsa people@199.99.999.99:/home/people/.ssh/authorized_keys
```
4. 之后再进行 
```bash
ssh people@199.99.999.99
```
	或者
```bash
scp /home/ryan/anyfile.txt people@199.99.999.99:/home/people/
```
	都不需要提供密码。