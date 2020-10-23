---
title: 在Ubuntu 16.04.6 LTS下使用Docker安装Oracle镜像及其简单的使用
tags: [Docker]
categories: Docker
---
>确定你的Ubuntu 16.04下已经安装Docker,没有安装的话可以看我以前的文章[Docker的入门](https://www.nonniexie.cn/article/20200709.html)。
### 1、查找oracle镜像
```
docker search oracle
```

![https://note.youdao.com/yws/api/personal/file/21F997DC5446493C90808ADBEEB1928C?method=download&shareKey=7aaf24fed0ab1676db2ed8cad5b0c840](https://note.youdao.com/yws/api/personal/file/21F997DC5446493C90808ADBEEB1928C?method=download&shareKey=7aaf24fed0ab1676db2ed8cad5b0c840)

### 2、拉取docker镜像并运行、进入
```
docker pull registry.aliyuncs.com/helowin/oracle_11g //拉取docker镜像
docker images //查看镜像是否下载成功
docker run -d -p 1521:1521 --name oracle registry.aliyuncs.com/helowin/oracle_11g //运行该镜像
docker exec -it oracle /bin/bash //进入容器
```

### 3、配置环境变量和修改账户密码
- 进入root账户`su root`,输入密码：`helowin`
- 编辑`/etc/profile`文件，并在文件的末尾添加下面内容
```

export ORACLE_HOME=/home/oracle/app/oracle/product/11.2.0/dbhome_2
export ORACLE_SID=helowin
export PATH=$ORACLE_HOME/bin:$PATH
source /etc/profile  //使修改的生效
```

- 切换`oracle`用户:`su oracle`   
- 使用`sqlplus`连接到`oracle`:`sqlplus /nolog → connect /as sysdba`
- 修改 sys 和 system 的密码并且修改密码的有效时间为无限
```
alter user system identified by oracle;
alter user sys identified by oracle;
ALTER PROFILE DEFAULT LIMIT PASSWORD_LIFE_TIME UNLIMITED;
```

![https://note.youdao.com/yws/api/personal/file/8988EBEA43AC46269F2FF954EE79E4BC?method=download&shareKey=0e7c34c2e28a3f5db230c354e4d8f301](https://note.youdao.com/yws/api/personal/file/8988EBEA43AC46269F2FF954EE79E4BC?method=download&shareKey=0e7c34c2e28a3f5db230c354e4d8f301)
