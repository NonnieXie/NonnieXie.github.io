---
title: Docker的使用
tags: [Docker]
categories: Docker
---
### 一、Docker的使用
#### 1.1、运行Hello World
在docker中可以在容器中运行应用程序,我们使用```docker run```命令来实现在一个容器中运行一个应用程序。
    ```
    docker run ubuntu /bin/echo "Hello world" //Docker 以 ubuntu镜像创建一个新容器，然后在容器里执行 bin/echo  "Hello world"，然后输出结果。
    ```
#### 2.1、运行交互式的容器
我们通过使用`-t -i`,来让docker运行的容器实现“对话”的功能：
    ```
    docker run -i -t ubuntu /bin/bash       
    //参数说明：        
            -t 在新容器内制定一个伪终端或终端      
            -i 允许你的容器内的标准输入进行交互       
    cat /proc/version  //查看当前系统的版本信息         
    ls //查看容器下的文件列表       
    ```

![运行交互式的容器](https://note.youdao.com/yws/api/personal/file/2394E7BEFB764405AFB082934354072B?method=download&shareKey=f890c55153028bd9d60524f9a95554cd)

#### 3.1、启动容器(后台模式)
可以使用下面命令来创建一个以进程方式运行的容器:     
```
    docker run -d ubuntu /bin/sh -c "while true; do echo hello world; sleep 1; done" //运行之后我们并没有看到输入“Hello world”,而看到的是容器的ID   
    docker ps  //查看确定容器是否在运行 
    //查看容器内的标准输出                    
    docker logs <容器ID>                      
    docker logs <自动分配的容器名称>  
    //删除一个容器
    docker rm -f <容器 ID>     
    //以清理掉所有处于终止状态的容器。     
    docker container prune      
```

### 二、容器使用
- 2.1、获取镜像 ```docker pull ubuntu```
- 2.2、启动容器 ```docker run -it ubuntu /bin/bash```
- 2.3、后台运行 ```docker run -itd --name ubuntu-test ubuntu /bin/bash    //设置容器名为ubuntu-test ```
- 2.3、启动已经停止的容器 
    ```
    docker ps -a //查看所有容器
    docker start <容器 ID>  //启动一个已停止的容器
    ```
- 2.4、停止一个容器 
    ```
    //停止容器
    docker stop <容器 ID>
    docker stop <自动分配的容器名称> 
    //重启容器
    docker restart <容器 ID>
    docker restart <自动分配的容器名称> 
    ```
- 2.5、进入后台容器
    ```
    docker ps //查看运行的容器
    docker attach <运行容器 ID> or <运行容器的容器名> 
    docker exec -it <运行容器 ID> /bin/bash  //使用exit或者ctrl +D退出，后台容器不会退出
    ```

- 2.6、导出和导入容器
    ```
    docker export <容器 ID> > ubuntu.tar  //导出容器
    cat /root/ubuntu.tar  |docker import - test/ubuntu:v1  //导入容器
    ```

- 2.7、查看端口的映射情况
    ```
    docker port <容器ID>
    docker port <自动分配的容器名称> 
    ```

>注意：如果你这里使用exit或者ctrl +D的话，后台运行的容器就会直接退出。推荐大家使用```docker exec```命令，因为此退出容器终端，不会导致容器的停止。

### 三、Docker镜像使用
当运行容器时，使用的镜像如果在本地中不存在，docker 就会自动从 docker 镜像仓库中下载，默认是从 Docker Hub 公共镜像源下载。
#### 3.1、列出镜像列表
在root用户下，我们可以通过使用```docker images```来列出本地主机上的镜像。
![Docker images 列出镜像](https://note.youdao.com/yws/api/personal/file/AA1D360E53344577BD3516E400D8A513?method=download&shareKey=001559875f7df3e7160281b8c4aaaa58)

还可以使用以下命令:
```
docker search ubuntu //查找镜像
docker pull ubuntu:13.10 //获取新的镜像
docker rmi hello-world //删除镜像
```