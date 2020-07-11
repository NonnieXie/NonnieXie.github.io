
博主以前是Hexo和GitHub来搭建的网站[nonniexie.cn](nonniexie.cn)的,这里介绍用Typecho来搭建。准备工作，需要一台自己的云服务器。并且远程连接到云服务器上，给你推荐几个比较好用的连接工具FinalShell、Xshell 5、SecureCRTP、putty一共四款工具。个人比较喜欢Xshell 5和FillalShell。
### 一、安装[宝塔面板](https://www.bt.cn/)
1. 首先远程连接云服务器
2. 在命令行输入:

     Centos安装脚本
     ```
    yum install -y wget && wget -O install.sh http://download.bt.cn/install/install_6.0.sh && sh install.sh
    ```
    Ubuntu/Deepin安装脚本
    ```
    wget -O install.sh http://download.bt.cn/install/install-ubuntu_6.0.sh && sudo bash install.sh
    ```
3. 注意安装完成后的地址、用户名和密码。如果登录不上，去放开端下面端口
    ```
    Bt-Panel: http://49.232.136.20:8888/05e1fe2d
    username: ts75d74o
    password: d170b182
    Warning:
    If you cannot access the panel, 
    release the following port (8888|888|80|443|20|21) in the security group
   ```

4. 成功登录到宝塔面板
5. 根据提示安装Nginx、Mysql、php


### 二、搭建基于Typecho的网站
1. 下载Typecho包 [http://typecho.org/download](http://typecho.org/download)
2. 寻找自己喜欢的模版[https://typecho.me/](https://typecho.me/)
3. 在宝塔面板点击【网站】，然后添加站点
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200505002044131.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjMwODEw,size_16,color_FFFFFF,t_70)
4. 在宝塔面板上点击【文件】，在创建网站的根目录下上传下载好的Typecho包和主题
	>注意：将Typecho包里面的文件拷贝到网站根目录下，而主题则在Typecho包里面的user下的themes里面

5. 在浏览器输入域名，进行安装Typecho和配置网站
6. 接下面的操作，参考主题的配置几乎都有的

