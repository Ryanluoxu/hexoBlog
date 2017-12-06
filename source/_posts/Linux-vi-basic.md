---
title: Linux - vi basic
date: 2017-12-02 03:50:28
categories: Linux
tags: [Linux, vi, command]
---


## Basic Command ##

### 打开文件 ###
打开 /d/blog/_config.yml
```bash
vi /d/blog/_config.yml
```

### 搜索 ###
搜索 theme: `/theme`
回车，按 `n` 搜索下一个，直到搜索到目标。
<!--more-->

### 进入插入模式 ###
按 `i` 进入插入模式。屏幕左下角会显示：
```bash
-- INSERT --
```
此时可以进行输入和删除。

### 保存及退出 ###
退出前，按 `esc` 离开插入模式。

- 不保存，退出: `：q!`
- 查看之后，没有做修改，直接退出: `:q`
- 保存: `:w`
- 保存修改，退出: `:wq` 或者 `ZZ`


## 命令模式（非插入模式）下 ##

### 移动 ###
- 下一页：`ctrl+b`
- 上一页：`ctrl+f`
- 至屏幕顶行：`H` 
- 至屏幕中间行：`M` 
- 至屏幕最后行：`L`

### 删除 ###
- 删除所在行：`dd`

### 复制，粘贴 ###
- 复制所在行：`yy`
- 复制以下#行（包括本行）：`#yy`
- 粘贴：`p`

