---
title: Linux下静态库与动态库的制作
tags: [Linux]
categories: Linux
---
### 一、静态库的制作
1. 命名规则
	
	>lib+库的名字+.a  例如：`libmytest.a`

2. 制作步骤
	2.1、.c文件生成对应的.o文件    `gcc   *.c   -c `
	2.2、将生成的.o文件打包 
	
	>ar  rcs  +  静态库的名字(libmytest.a)   +   生成的所有的.o
	
3. 发布和使用静态库
	3.1、发布静态库(lib)
	4.2、头文件(include)
	
	用户的使用有下面两种使用方式：
	
	```
	gcc  + 源文件 +  静态库文件 -o +可执行程序 -I头文件
	gcc  main.c   lib/libtest.a   -o   sum   -Iinclude

	gcc  + 源文件 -I头文件 -L   静态库的目录 + 库名 -o+ 可执行程序
	gcc   main.c   -Iinclude  -L   lib   -l   MyCalc   -o   app
	```

4. 查看静态库
	
	>nm+静态库   ` nm libMyCalc.a` 
	>nm+可执行程序


5. 静态库的优缺点
	>优点：
	a、发布程序的时候。不需要提供对应的库
	b、加载库的速度
	缺点：
	a、库被打包到应用程序中，导致库的体积很大
	b、库发生了变化，需要重新编译程序

 6. 实现过程过程：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200422234406406.bmp?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjMwODEw,size_16,color_FFFFFF,t_70)

### 二、动态库的制作

1. 命名规则
	
	>lib+库的名字+.so  (类似与Windows下的dll文件)  
2. 制作步骤
	2.1、生成与位置无关的代码(生成与位置无关的.o)     `gcc -fPIC -c *.c -I../include`
	2.2、将.0打包成共享库(动态库)
	`gcc -shared -o libMyCalc.so *.o -I../include`
3. 发布和使用静态库
	3.1、发布静态库(lib)
	4.2、头文件(include)
	
	用户的使用方式有下面两种：
	```
	gcc  + 源文件 +  动态库文件 -o +可执行程序 -I头文件
	gcc main.c lib/libtest.so -o app -Iinclude  //运行./app,正确

	gcc  + 源文件 -I头文件 -L   动态库的目录 + 库名 -o+ 可执行程序
	gcc main.c -Iinclude -L lib -l MyCalc -o app   //运行./app，错误无法找到动态链接库
	```
	
	![在这里插入图片描述](https://img-blog.csdnimg.cn/20200422235157315.bmp)

4. 解决动态库失败的问题

- 1)、放到库目录中（**不推荐使用**）
将动态库cp(拷贝)到系统lib下`sudo cp lib/libMyCalc.so /lib`,可以通过`ldd 可执行文件`来查看
这样存在缺点，如何你自己的动态库和系统的动态库一样这样不就是存在错误。**不推荐使用**
- 2)、临时设置
配置LD_LIBRARY_PATH环境变量，将动态库的路径配置到环境变量中

	```
	echo $LD_LIBRARY_PATH //打印环境变量
	export  LD_LIBRARY_PATH=相对路径
	export  LD_LIBRARY_PATH=./lib
	这样的设置是临时的.在终端关闭设置就会失效，在制作的过程中使用。
	```

- 3)、不常用的方法（**永久设置**）
修改家目录下.bashrc的配置文件的内容，在修改完成之后需要重启终端
在最后一行添加：`export  LD_LIBRARY_PATH=绝对路径` 
```export  LD_LIBRARY_PATH=/home/ubuntu/Linux代码/Calc```
- 4)、需要找到动态连接器的配置文件，将动态库的路径写到配置文件中，然后在进行更新已经显示操作
使用命令`sudo ldconfig -v`
```sudo vim /etc/ld.so.conf```

5. 动态库的有点
	>优点：
	a、执行程序体积小
	b、函数接口不变的情况下，动态库更新了，不需要编译程序
	缺点：
	a、发布时需要将动态库提供给用户
	b、动态库没有被打包到应用程序中，加载速度相对比较慢

	
	

