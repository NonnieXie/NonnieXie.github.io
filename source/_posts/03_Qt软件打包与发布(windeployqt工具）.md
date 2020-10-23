---
title: 03_Qt软件打包与发布(windeployqt工具）
tags: [Qt]
categories: Qt
---
使用官方自带的windeployqt工具来打包我们的项目。
### 一、查看windeloyqt工具在哪
我的Qt安装在D盘，所以我知道到的目录在`D:\Qt\Qt5.8.0\5.8\mingw53_32\bin`
### 二、生成项目的release文件
打开你的项目，选择release版本，点击运行，就能够生成项目的release版本的可执行程序了。
### 三、打开Qt的控制台，打包
>注意是Qt的控制台，不是dos界面。

![qt的控制台](https://note.youdao.com/yws/api/personal/file/DF8E8FBD58B34012BDFA99EBAA33E6FD?method=download&shareKey=8ac24e1553be865a0fc0cdba6c1205d6)

将你生成的Release版的可执行程序移动到一个新的文件夹中，切换到当前的目录下，接下来使用`windeployqt 程序名`命令，就可以对程序进行打包操作，如图：

![windeployqt命令](https://note.youdao.com/yws/api/personal/file/0CDF5BA8B10248AE8DA0BA62FBF93417?method=download&shareKey=c215cc7c7ac20720a23f5b0605f86fa8)