---
title: 在Ubuntu 16.04.6 LTS下使用Docker安装Ubuntu、CetOS和MySQL镜像及其简单的使用
tags: [Docker]
categories: Docker
---
>确保你的系统下安装有Docker,切换到`root`账户下，如果是普通用户，下面的指令操作需要在指令前添加`sudo`.
### Docker的安装实例
#### 1、Docker安装Ubuntu

 ```
    docker search ubuntu  //搜索ubuntu镜像
    docker pull ubuntu //拉取最新版的 Ubuntu 镜像
    docker images  //查看本地镜像
    docker run -itd --name ubuntu-test ubuntu  //启动容器，并将容器的名字改为ubuntu-test 
    docker exec -it ubuntu-test  /bin/bash  //进入启动的容器下
    docker ps //查看容器的运行信息
 ```


#### 2、Docker安装CentOS
```
    docker search centos   //搜索centos  镜像
    docker pull centos:centos7 //拉取指定版本的 CentOS 镜像，这里我们安装指定版本为例(centos7):
    docker images  //查看本地镜像
    docker run -itd --name centos-test centos:centos7 //运行容器
    docker exec -it centos-test  /bin/bash
    docker ps //查看容器的运行信息
```

#### 3、Docker安装MySQL
```
    docker search mysql //查看可用的 MySQL 版本
    docker pull mysql:latest 拉取 MySQL 镜像
    docker images  //查看本地镜像
    #启动
    docker run --name mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123456 -d mysql
    //参数说明：
        -p 3306:3306 ：映射容器服务的 3306 端口到宿主机的 3306 端口，外部主机可以直接通过 宿主机ip:3306 访问到 MySQL 的服务。
        -e MYSQL_ROOT_PASSWORD=123456：设置 MySQL 服务 root 用户的密码。
        -d 后台运行容器，并返回容器的ID
    docker ps //查看容器的运行信息  
    #进入容器
    docker exec -it mysql /bin/bash

    #登录mysql
    mysql -u root -p
    ALTER USER 'root'@'localhost' IDENTIFIED BY '123456'; 、、

    #添加远程登录用户
    CREATE USER 'salt'@'%' IDENTIFIED WITH mysql_native_password BY '123456';
    GRANT ALL PRIVILEGES ON *.* TO 'salt'@'%';
```