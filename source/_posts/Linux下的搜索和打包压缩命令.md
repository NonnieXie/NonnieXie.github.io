---
title: Linux下的搜索和打包压缩命令
tags: [Linux]
categories: Linux指令
---
### 一、文件的查找
#### 1. 按文件属性查找:   

1). **文件名:find + 查找的目录 + -name + "文件的名字"**   

```
  find ~ -name "test.c" 
  find ~ -name "*.c"    //*通配符  ~表示家目录   /home/salt
```

2). **文件大小: find + 查找目录 + -size + +10k**    

```
说明: +表示大于 -表示小于 k为小写 M为大写
    find ~ -size +10k   //文件>10k   
    find ~ -size -10k   //文件<10k
    find ~ -size  +10K -size -100k  //10k<文件<100k
```

3). **文件类型: find + 查找目录 + -type + d/f/b/c/s/p/l**

文件类型 | 符号
---|---
普通文件|- (在搜索是用f)
目录|d
链接符号|l
块设备|b
字符设备|c
socket文件|s
管道|p(mkfifo创建管道)

#### 2. 按文件内容查找:
grep -r "查找的内容" + 查找的路径

```
grep -r "stdio.h" ~   //在家目录下查找有stdio.h的文件
```

### 二、解压工具
#### 1、屌丝版

```
1. gzip 文件名  
撤销压缩使用：gunzip 文件名
不打包压缩,不保留原文件,不压缩目录,将文件压缩为.gz格式
2. bzip2 文件名
保留原文件：bzip -k 文件名
撤销压缩使用：bunzip2 文件名
不打包压缩,不压缩目录,将文件压缩为.bz2格式
```

#### 2、高富帅版
1、tar不使用z/j,该命令只是将文件或者目录进行打包操作

```
参数:
    c-- 创建  >>>压缩
    x-- 释放  >>>解压缩
    v-- 显示提示信息 --压缩解压缩 --可以对其进行省略
    f-- 指定压缩文件的名字
    
    z-- 使用屌丝版本gzip的方式进行文件压缩 --.gz
    j-- 使用吊丝版本bzip2的方式进行文件压缩 --.bz2
压缩：
    tar zcvf 生成压缩文件的名字(xxx.tar.gz) 要压缩的文件或者目录
    tar jcvf 生成压缩文件
解压缩：
    tar jxvf 压缩的名字(解压到当前目录)
    tar jxvf 压缩包名字 -C 压缩的目录
```

2、rar必须自己手动安装sudo apt-get install rar

```
参数：
    压缩:a
    解压缩:x
压缩:
    rar a 压缩包名(不需要带.rar会自动补全的) 需要压缩的文件或者目录
解压缩：
    rar x 压缩包文件名(xxx.rar)   //解压到当前目录下
    rar x 压缩包文件名(xxx.rar)  目录(test) //解压到指定的test目录下
```

3、zip必须自己手动安装sudo apt-get install zip

```
压缩:
    zip 压缩包的名字 压缩的文件或者目录
解压缩：
    unzip 压缩包的名字   //解压到当前目录下
    unzip 压缩包的名字 -d 解压的路径
```

>总结：   
>    相同之处：     
>tar/rar/zip 参数 生成的压缩文件的名字  压缩的文件或者目录 --压缩的时候的语法     
>tar/rar/zip 参数 压缩包的名字 参数(rar没有参数) 解压缩目录 --解压语法

### 三、软件的安装
#### 1、在线安装
##### apt-get安装

```
sudo apt-get install update //更新软件列表
sudo apt-get insatll tree //安装
sudo apt-get remove  tree //卸载
sudo apt-get clear //清除软件的安装包 实际就是清除：/var/cache/apt/archives目录下的.deb文件
sudo apt-get install aptitude  //安装aptitude下载工具
```

##### aptitude安装

```
sudo aptitude insatll tree  //安装
sudo aptitude remove  tree  //移除
sudo apt-get install aptitude  //重新安装
sudo aptitude show  tree //显示当前软件的状态
```

#### 2、deb包安装

```
sudo dpkg -i xxx.deb //安装
sudo dpkg -r xxx    //卸载
```

#### 3、源码安装
这里我不常用，后期用到在进行补充。





有关Linux下的指令请参看：
[https://cloud.tencent.com/developer/article/1498762](https://cloud.tencent.com/developer/article/1498762)
