---
title: Docker入门
tags: [Docker]
categories: Docker
---

>前提：我们初学`docker`的话,我们需要熟悉`Linux`的命令和背景知识，及其`git`的相关知识。推荐一本书
[Docker基础与实战](https://www.jianguoyun.com/p/DY0m0MsQjKL5BxizxKoD) (访问密码 : 2vfnt5)
***************
### 一、Docker教程
`Docker` 是一个开源的应用容器引擎，基于 `Go` 语言 并遵从 `Apache2.0` 协议开源。`Docker` 可以让开发者打包他们的应用以及依赖包到一个轻量级、可移植的容器中，然后发布到任何流行的 Linux 机器上，也可以实现虚拟化。
#### 1、Docker的优点
`Docker` 是一个用于开发，交付和运行应用程序的开放平台。`Docker` 使您能够将应用程序与基础架构分开，从而可以快速交付软件。借助 Docker，您可以与管理应用程序相同的方式来管理基础架构。通过利用 `Docker` 的方法来快速交付，测试和部署代码，您可以大大减少编写代码和在生产环境中运行代码之间的延迟。
#### 2、Docker容器技术和传统虚拟机技术的性能比较
|特性|容器|虚拟机|
|---|---|---|
|启动速度|秒级|分钟级|
|硬盘使用|一般为MB|一般为GB|
|性能|接近原生|弱于|
|系统支持量|单机支持上千个容器|一般几十个|
|隔离性|安全隔离|完全隔离|

#### 3、Docker的相关链接
Docker官网：[https://www.docker.com/](https://www.docker.com/)  
Github Docker 源码：[https://github.com/docker/docker-ce](https://github.com/docker/docker-ce)

 **********************

### 二、Docker的安装
Docker支持在主流的操作系统平台上使用，包括Ubuntu、CentOS、Windows和MacOS系统。这里我主要是Ubuntu使用来进行其他的系统安装可以参考[https://www.runoob.com/docker/ubuntu-docker-install.html](https://www.runoob.com/docker/ubuntu-docker-install.html)
#### 2.1、使用官方安装脚本自动安装
```
curl -fsSL https://get.docker.com | bash -s docker --mirror Aliyun
//也可以使用国内 daocloud 一键安装命令
curl -sSL https://get.daocloud.io/docker | sh
```
#### 2.2、使用Docker仓库进行安装
1. 选择国内的云服务商，这里选择阿里云为例    
    ```
    curl -sSL http://acs-public-mirror.oss-cn-hangzhou.aliyuncs.com/docker-engine/internet | sh -
    ```

2. 安装所需要的包
    ```
    sudo apt-get install linux-image-extra-$(uname -r) linux-image-extra-virtual
    ```
3. 添加使用 HTTPS 传输的软件包以及 CA 证书
    ```
    sudo apt-get update
    sudo apt-get install apt-transport-https ca-certificates
    ```
4. 添加GPG密钥
    ```
    sudo apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
    ```
5. 添加软件源
    ```
    echo "deb https://apt.dockerproject.org/repo ubuntu-xenial main" | sudo tee /etc/apt/sources.list.d/docker.list
    ```
6. 添加成功后更新软件包缓存
    ```
    sudo apt-get update
    ```
7. 安装docker
    ```
    sudo apt-get install docker-engine
    ```
8. 启动 docker
    ```
    sudo systemctl enable docker
    sudo systemctl start docker
    ```
9. 测试运行
    ```
    sudo docker run hello-world
    ```
 


**************
### 三、Docker镜像加速
我们一般在`DockerHub`拉取镜像有时会遇到困难，此时我们就需要配置加速器。这里我使用国内加速器服务，阿里云：```https://<你的ID>.mirror.aliyuncs.com```
>没有阿里云的自己去注册一个自己的阿里云账户。

针对Docker客户端版本大于 1.10.0 的用户   

您可以通过修改`daemon`配置文件```/etc/docker/daemon.json```来使用加速器

    ```
    sudo mkdir -p /etc/docker
    sudo tee /etc/docker/daemon.json <<-'EOF'
    {
    "registry-mirrors": ["https://nw5iareo.mirror.aliyuncs.com"]
    }
    EOF
    sudo systemctl daemon-reload
    sudo systemctl restart docker
    docker info ///显示 Docker 系统信息
    ```