---
title: 使用Hexo+Github搭建自己的个人博客
tags: [hexo,BlueLake]
categories: Hexo博客折腾
top: true
---
#### 1、准备工作
 1、创建一个[GitHub](https://github.com/)账户

 2、下载安装 [ Node.js](https://nodejs.org/) (包含 npm)

 3、安装[Git](https://git-scm.com/) 
#### 2、打开git bash命令行输入:
>注:在任意位置打开git bash输入即可。
```bash
node -v  //查看node.js的版本号
npm -v   //查看npm的版本号
npm install -g cnpm --registry=https://registry.npm.taobao.org   //安装cnpm淘宝源
cnpm -v  //查看版本号
cnpm install -g hexo-cli  //安装hexo博客框架
hexo -v //查看hexo的版本号
```
#### 3、新建本地博客文件夹Blog
>注：在电脑上自己找一个位置，进行新建文件夹Blog。

```bash
hexo init //初始化博客
cnpm install --save hexo-deployer-git //安装git部署插件
hexo server //开启本地预览服务
hexo generate //生成静态文件
hexo deploy //部署到远程站点
```

> 在Blog目录下先进行初始化`hexo init` ,然后安装：`cnpm install --save hexo-deployer-git`

![在Bolg目录下安装](https://img-blog.csdnimg.cn/20200225232705464.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjMwODEw,size_16,color_FFFFFF,t_70)
#### 4、GitHub新建仓库
打开[https://github.com/new](https://github.com/new)来创建自己的仓库。
![创建博客](https://img-blog.csdnimg.cn/20200226113103483.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjMwODEw,size_16,color_FFFFFF,t_70)
修改Bolg目录下的，_config.yml文件
![修改目录下的_config.yml文件](https://img-blog.csdnimg.cn/20200226113942664.png)

>注意：仓库的地址可以是使用https协议也可以使用ssh协议。区别在于使用https协议每次部署需要输入
>GitHub的账户名和密码密码。

这里我使用的HTTPS协议，接下来命令行输入：`hexo d`进行部署；
>注意下来需要输入你的GitHub用户名和密码。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200226114503708.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjMwODEw,size_16,color_FFFFFF,t_70)
![本地浏览](https://img-blog.csdnimg.cn/20200410210016199.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjMwODEw,size_16,color_FFFFFF,t_70)
更换自己喜欢的主题：
git clone https://github.com/chaooo/hexo-theme-BlueLake.git themes/BlueLake
参看下面链接进行配置
[https://github.com/chaooo/hexo-theme-BlueLake](https://github.com/chaooo/hexo-theme-BlueLake)
[https://blog.luuman.club/2015/12/27/GitHubHexo/](https://blog.luuman.club/2015/12/27/GitHubHexo/)

