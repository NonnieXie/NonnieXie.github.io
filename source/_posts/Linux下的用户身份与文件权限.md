---
title: Linux下的用户身份与文件权限
tags: [Linux]
categories: Linux指令
---

## 一、用户管理
	创建用户
		sudo adduser + 用户名（luffy）
		sudo useradd -s /bin/bash -g itcast -d /home/itcast -m itcast
			-s 指定新用户登陆时shell类型
			-g 指定所属组，该组必须已经存在
			-d 用户家目录
			-m 用户家目录不存在时，自动创建该目录
	设置用户组
		sudo groupadd itcast
	删除用户
		sudo deluser + 用户名（luffy）
		sudo userdel -r itcast
			选项 -r 的作用是把用户的主目录一起删除
	切换用户
		su + 用户名（sanji）
	root用户
		sudo su
	设置密码
		sudo passwd + 用户名（luffy）
		sudo passwd root
		sudo passwd
		设置root密码
	退出登录用户
		exit