---
title: Git的安装与使用
tags: [git,开发工具]
categories: 开发工具
top: true
---
说明：此文章是学习黑马程序员Git零基础入门到实战详解整理的笔记，主要是Windowns下Git的安装、基本使用、分支管理、版本回退、冲突解决、GUI工具的介绍、文件忽略机制等。如想在Linux平台下安装Git 查看通过[https://blog.csdn.net/qq_43630810/article/details/104483007](https://blog.csdn.net/qq_43630810/article/details/104483007)来进行安装。
#### 一、Git基础
Git是目前世界上最先进的分布式版本控制系统，用于敏捷高效地处理任何或小或大的项目。
###### 1、谈谈Git与SVN的区别
 1. **Git是分布式的，svn是集中式的**：这个是Git和其他非分布式的版本控制系统的，最主要的区别。
 2. **Git把内容按元数据方式存储，而SVN是按文件**：所有的资源控制系统都是把文件的元信息隐藏在一个类似.svn、.git的文件中
 3. **Gitf分支和SVN的分支不同**：分支在SVN中一点都不特别，其实它就是版本库中的另一个目录
 4. **Git没有一个全局的版本号，而SVN有**：目前为止这是SVN相比Git缺少最大的一个特征
 5. **Git的内容完整性要优于SVN**：Git 的内容存储使用的是 SHA-1 哈希算法。这能确保代码内容的完整性，确保在遇到磁盘故障和网络问题时降低对版本库的破坏。
![SVN集中式管理系统](https://img-blog.csdnimg.cn/20200225200234787.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjMwODEw,size_16,color_FFFFFF,t_70)
![git分布式管理控制系统](https://img-blog.csdnimg.cn/20200225200308575.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjMwODEw,size_16,color_FFFFFF,t_70)
###### 2、SVN的弊端与Git的好处
>SVN弊端：
>1、中央服务器坏了，一切OVER
>2、所有的上传和下载都是基于文件传输方式完成的，速度会慢


>git好处
>1、无需连网也能记录查看历史版本信息
>2、无需过多依赖中央仓库，每个人本地也有全部的信息
>向中央仓库传输内容依托的是文件流传输，速度比SVN块N倍
###### 3、Git与GitHub
Git的安装与GithHub账户的注册不做介绍。
**1 、两者区别**
Git([https://git-scm.com/](https://git-scm.com/))是一个分布式版本控制系统，简单的说其就是一个软件，用于记录一个或若干文件内容变化，以便将来查阅特定版本修订情况的软件。

Github（[https://www.github.com](https://www.github.com)）是一个为用户提供Git服务的网站，简单说就是一个可以放代码的地方（不过可以放的当然不仅是代码）。Github除了提供管理Git的web界面外，还提供了订阅、关注、讨论组、在线编辑器等丰富的功能。Github被称之为全球最大的基友网站。
#### 二、Git的使用过程
##### 1、本地仓库
###### 1.1、工作流程
Git本地操作分为三个区域：

工作流程：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200224154216190.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjMwODEw,size_16,color_FFFFFF,t_70)
工作流程：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200224154313643.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjMwODEw,size_16,color_FFFFFF,t_70)
###### 1.2、本地仓库操作

什么是仓库呢？仓库又名版本库，英文名repository，我们可以简单理解成是一个目录，用于存放代码的，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改、删除等操作Git都能跟踪到。

①在安装好后首次使用我们需要进行全局配置
在桌面空白处右键，点击“Git Bash Here” 已打开Git命令行窗口

```bash
$ git config --global user.name "用户名"
$ git config --global user.email "邮箱地址"
$ git config --list
```

> 注意：配置完成后输入git config --global user.name和git config --global user.email进行查看，是否是自己所绑定的。

②创建仓库
当我们需要让Git去管理某个项目的时候，就需要创建仓库了。在创建仓库时使用的目录不一定要求是非空的目录，但是最好使用一个非空的目录。

> 注意：在使用过程中最好不要使用包含中文的目录名（目录亦是如此）。

a、创建空目录：mkdir pro_git
b、进入项目目录中：cd pro_git
c、Git仓库初始化：（让Git知道，它需要来管理这几个目录）
	 指令：git init
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200224160427637.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjMwODEw,size_16,color_FFFFFF,t_70)
③Git常用指令操作
查看当前状态：git status 【非必要】
添加到缓存区：git add 文件名
```bash
说明：git add指令，可以添加一个文件，也可以同时添加多个文件。
语法1：git add 文件名
语法2：git add 文件名1 文件名2 文件名3 …
语法3：git add .					【添加当前目录到缓存区中】
```
提交至版本库：git commit -m “注释内容”
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200224161027746.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjMwODEw,size_16,color_FFFFFF,t_70)
###### 1.3、版本回退
版本回退分为两步骤进行操作：

```bash
步骤：
	①查看版本，确定需要回到的时刻点
			指令：
				git log
				git log --pretty=oneline
	②回退操作
			指令：
				git reset --hard 提交编号
```
案例：查看版本和回退到创建第一个文件readme.txt的版本。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200224161625191.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjMwODEw,size_16,color_FFFFFF,t_70)


> 注意:回退到过去的版本，要想在回到之间最新的版本的时候。可以通过之间查看的的提交码回到最新版本，也可以使用(*git reflog*)指令去查看历史操作，以得到最新的commit ID。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200224162340293.png)
##### 2、远程仓库
主要以GitHub为例。
######  2.1、GithHub创建
打开创建仓库页面：[https://github.com/new](https://github.com/new)
圈出的部分为必填项，其余根据实际需要选择性补充：
![Github创建仓库](https://img-blog.csdnimg.cn/20200224192826877.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjMwODEw,size_16,color_FFFFFF,t_70)

> 注意：仓库名要在当前用户下唯一。

###### 2.2 、两种不同的使用方式
2.2.1、基于http/https协议
a、创建空目录，名称为shop
![创建空目录](https://img-blog.csdnimg.cn/20200224193635888.png)
b、使用clone指令克隆线上仓库到本地
语法：git clone  线上仓库
![克隆线上仓库](https://img-blog.csdnimg.cn/20200224194232490.png)

c、在仓库上做对应的操作（提交暂存区、提交本地仓库、提交线上仓库、拉取线上仓库）
提交到线上仓库的指令：git push
拉取线上仓库：git pull
![提交到线上仓库](https://img-blog.csdnimg.cn/20200224195206506.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjMwODEw,size_16,color_FFFFFF,t_70)

> 提醒：在以后每天工作中第一件事就是先git pull拉取线上最新的版本；而下班前要做的是git push，将本地的代码提交到线上仓库。

2.2.2、基于ssh协议（推荐）
该方式与前面https方式相比，此方式影响github对于用户的身份鉴权方式，对于git的具体操作（如提交本地、添加注释、提交远程等操作）没有任何影响。

①生成公私玥对指令（需先OpenSSH安装，若是没有联系我）：ssh-keygen -t rsa -C “注册邮箱”
![OpenSSH公私钥](https://img-blog.csdnimg.cn/20200224201842503.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjMwODEw,size_16,color_FFFFFF,t_70)
②上传公钥内容（id_rsa.pub）
![上传公钥内容](https://img-blog.csdnimg.cn/20200224204158846.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjMwODEw,size_16,color_FFFFFF,t_70)
③执行后续git的操作
a、clone线上仓库到本地（git clone）
![SSH克隆线上仓库](https://img-blog.csdnimg.cn/20200224205618772.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjMwODEw,size_16,color_FFFFFF,t_70)
b、修改文件后添加缓存区、提交本地仓库、提交线上仓库
![SSH添加新文件](https://img-blog.csdnimg.cn/20200224205747971.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjMwODEw,size_16,color_FFFFFF,t_70)
*在git push的时候并没有提示要求我们输入帐号密码，说明公私玥已经实现了用户身份鉴权*。
###### 2.3、分支管理
什么是分支？
![分支管理](https://img-blog.csdnimg.cn/20200224210447494.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjMwODEw,size_16,color_FFFFFF,t_70)
      在版本回退中，每次提交后都会有记录，Git把它们串成时间线，形成类似于时间轴的东西，这个时间轴就是一个分支，我们称之为==master分支==。
     而在开发的时候往往是团队协作，多人进行开发，因此光有一个分支是无法满足多人同时开发的需求的，并且在分支上工作并不影响其他分支的正常使用，会更加安全，Git鼓励开发者使用分支去完成一些开发任务。
 
```bash
分支相关指令：
查看分支：git branch
创建分支：git branch 分支名
切换分支：git checkout 分支名 
删除分支：git branch -d 分支名
合并分支：git merge 被合并的分支名
```
查看分支：
![查看分支](https://img-blog.csdnimg.cn/20200224211033367.png)
> 注意：当前分支前面有个标记“*”；

创建分支：
![创建分支](https://img-blog.csdnimg.cn/20200224211354922.png)
切换分支：
![切换分支](https://img-blog.csdnimg.cn/20200224211544583.png)
合并分支：
现在先将dev分支下的readme文件中添加一行并提交到本地
![dev分支下添加](https://img-blog.csdnimg.cn/20200224234057493.png)
切换到master分支下观察readme文件的内容
![master分支](https://img-blog.csdnimg.cn/20200224235124876.png)
将dev分支的内容和master分支合并：
![合并分支](https://img-blog.csdnimg.cn/20200224235401176.png)
删除分支：
![删除分支](https://img-blog.csdnimg.cn/20200224235535595.png)
>注意：在删除分支的时候，一定要先退出要删除的分支，然后才能删除。

合并所有分支之后，需要将master分支提交线上远程仓库中：
![提交到线上仓库](https://img-blog.csdnimg.cn/20200225000649744.png)

###### 2.4、冲突的产生与解决

案例：模拟产生冲突。
①下班之后同事在线上仓库进行修改
![线上修改](https://img-blog.csdnimg.cn/2020022515324582.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjMwODEw,size_16,color_FFFFFF,t_70)
>注意：此时我的本地仓库的内容和线上不一致的。

![线上和线下的区别](https://img-blog.csdnimg.cn/20200225153722804.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjMwODEw,size_16,color_FFFFFF,t_70)
②第二天上班的时候，没有拉取线（git pull）上的文件，而直接修改了本地所对应的文件内容。
![修改readm.txt文件](https://img-blog.csdnimg.cn/20200225191619228.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjMwODEw,size_16,color_FFFFFF,t_70)
③在下班的时候将文件推送到线上仓库（git push）
![修改完本地推向线上](https://img-blog.csdnimg.cn/2020022519135988.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjMwODEw,size_16,color_FFFFFF,t_70)
>提示我们要在再次push之间先git pull操作。

==【解决冲突】==
④先git pull
![解决冲突拉取线上仓库文件](https://img-blog.csdnimg.cn/20200225191822755.png)
⑤打开冲突文件，解决冲突
解决方法：需要和同事进行商量，看代码如何保留，然后将改好的文件再次提交即可。
![冲突文件合并](https://img-blog.csdnimg.cn/20200225192054373.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjMwODEw,size_16,color_FFFFFF,t_70)
⑥重新提交
![重新提交解决冲突文件](https://img-blog.csdnimg.cn/20200225192448762.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjMwODEw,size_16,color_FFFFFF,t_70)
⑦查看线上效果
![解决冲突后的线上效果](https://img-blog.csdnimg.cn/20200225192641491.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjMwODEw,size_16,color_FFFFFF,t_70)
>新手小技巧：上班第一件事先git pull,可以在一定程度上避免冲突的产生。

#### 三、实用技能
##### 1、图形管理工具
###### 1.1、GitHub for Dektop
Github出品的软件，功能完善，使用方便。对于经常使用GitHub的开发人员来说是非常便捷的工具。界面干净，用起来非常顺手，顶部的分支时间线非常绚丽。
###### 1.2、Source tree
老牌的Git GUI管理工具了，也号称是最好用的Git GUI工具。功能丰富，基本操作和高级操作都非常流畅，适合初学者上手。
###### 1.3、TortoiseGit
对于熟悉SVN的开发人员来说，这个小乌龟图标应该是非常友善了。TortoiseGit 简称 tgit, 中文名海龟Git。它与其前辈TortoiseSVN都是非常优秀的开源版本控制客户端软件。
##### 2、忽略文件
场景：在项目目录下有很多万年不变的文件目录，例如css、js、images等，或者还有一些目录即便有改动，我们也不想让其提交到远程仓库的文档，此时我们可以使用“忽略文件”机制来实现需求。

忽略文件需要新建一个名为==.gitignore==的文件，该文件用于声明忽略文件或不忽略文件的规则，规则对当前目录及其子目录生效。
注意：该文件因为没有文件名，没办法直接在windows目录下直接创建，可以通过命令行Git Bash来touch创建。

常见规则写法有如下几种：
```
1）/mtk/               过滤整个文件夹
2）*.zip                过滤所有.zip文件
3）/mtk/do.c           过滤某个具体文件
4) !index.php			   不过滤具体某个文件	
```
在.gitignore文件中，以#开头都是注释。
案例：
①先在本地创建一个js目录以及目录中的js文件
![本地创建js](https://img-blog.csdnimg.cn/20200225164330578.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjMwODEw,size_16,color_FFFFFF,t_70)
②依次提交本地和线上
![依次提交本地和线上](https://img-blog.csdnimg.cn/20200225164734502.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjMwODEw,size_16,color_FFFFFF,t_70)
③创建.gitignore文件并编写文件中的规则
![创建.gitignore文件](https://img-blog.csdnimg.cn/20200225163843486.png)
④再次提交本地和线上
![提交本地和线上index.js](https://img-blog.csdnimg.cn/20200225170844874.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjMwODEw,size_16,color_FFFFFF,t_70)
⑤并观察本地和线上的仓库是否有新加的index.js文件
![线上仓库查看](https://img-blog.csdnimg.cn/20200225171221967.png)
![本地文件](https://img-blog.csdnimg.cn/20200225165725541.png)
由于我本地安装的工具是TortoiseGit，明显的看出来index.js文件是被忽略的文件。




