---
title: Hexo-Next 添加 Gitment 评论系统
date: 2017-11-27 23:05:32
categories: 搭建博客
tags: [Hexo, Nexy, 博客, 主题优化, 评论, Gitment]
---

**声明：本文为 ryanluoxu 原创文章，欢迎转载，请在明显位置注明出处。**

网上关于添加 Gitment 的博客不少，但是互相有些出入。
由于 Next 更新，Gitment 已经预置了，所以不需要自己再添加代码。
这里分享我自己的设置经过，参考的文章在文末。

## 注册 OAuth Application ##

1. 登录 Github。
2. 前往 https://github.com/settings/profile
3. 点击左侧下方的 ` Developer settings` 
4. 点击绿色 `Register a new application`
5. 填写以下内容：
	```
	Application name：Gitment
	Homepage URL：https://ryanluoxu.github.io/
	Application description：Blog comment system
	Authorization callback URL：https://ryanluoxu.github.io/
	```
6. 点击 `Register application`
7. 得到：
	```
	Client ID:
	Client Secret:
	```
<!--more-->
## 创建存放 gitment-comments 的 repository ##

1. 创建 repository。 Repository name 为 gitment-comments
2. 地址：https://github.com/Ryanluoxu/gitment-comments.git
3. 但是稍后填的是 `gitment-comments`，不是地址。

## 添加 Gitment 到博客 ##

1. 打开 D:\blog\themes\next\_config.yml
2. 找到 `Gitment`
3. 如下修改：
```
gitment:
  enable: true
  mint: true 		# RECOMMEND, A mint on Gitment, to support count, language and proxy_gateway
  count: true 		# Show comments count in post meta area
  lazy: false 		# Comments lazy loading with a button
  cleanly: false 	# Hide 'Powered by ...' on footer, and more
  language: 		# Force language, or auto switch by theme
  github_user: ryanluoxu 	# 此处 - Your Github ID
  github_repo: gitment-comments # 此处注意 - The repo you use to store Gitment comments
  client_id: xxxxxxxxxxxxxxxxxx # 此处 - Github client id for the Gitment
  client_secret: xxxxxxxxxxxxx # 此处 - Github access secret token for the Gitment
  proxy_gateway: # Address of api proxy, See: https://github.com/aimingoo/intersect
  redirect_protocol: # Protocol of redirect_uri with force_redirect_protocol when mint enabled

```
4. 之后生成并且部署才会生效，本地有时没有效果 
```
hexo g -d
``` 
	部署之后，有可能碰到 `Not Found Error`，先不要着急，等一段时间再看看。
5. 之后文章底部会出现 `初始化本文的评论页`，点击初始化。

## 参考 ##

[Gitment：使用 GitHub Issues 搭建评论系统](https://imsun.net/posts/gitment-introduction/)
[hexo next主题集成gitment评论系统](http://yangq.me/post/ab9bb85a.html)
[Hexo Next 主题博客添加gitment评论功能](https://icessun.github.io/Hexo-Next-%E4%B8%BB%E9%A2%98%E5%8D%9A%E5%AE%A2%E6%B7%BB%E5%8A%A0gitment%E8%AF%84%E8%AE%BA%E5%8A%9F%E8%83%BD.html)
[为 hexo NexT 添加 Gitment 评论插件](https://meesong.github.io/StaticBlog/2017/NexT+Gitment/)