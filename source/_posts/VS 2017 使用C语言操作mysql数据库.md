---
title: VS 2017 使用C语言操作mysql数据库
tags: [MySql]
categories: C语言
---
### 一、在操作之间首先安装软件：    
1、Windows下[安装MySQL数据库](https://www.runoob.com/w3cnote/windows10-mysql-installer.html)  
2、安装Visual Studio 2017
### 二、VS 2017环境配置
1. 点击项目->项目属性，操作如图:   
![打开项目属性页](https://note.youdao.com/yws/api/personal/file/C5527E27D2984128B956908ED56E225A?method=download&shareKey=d623c6fe814b9a1780d87833b03c45c8)   
2、选择C/C++,在常规的附加包含目录添加mysql安装地址中include文件的地址，如我的地址是`C:\Program Files\MySQL\MySQL Server 5.7\include`,如图：    
![修改附加包含目录](https://note.youdao.com/yws/api/personal/file/8F67C64106FE410F811F1E971E9F9434?method=download&shareKey=cd26799cb175222f77f8c982bd8aaaa5)

3. 选择链接器，在常规中附加目录中添加mysql安装地址lib文件的地址，如我的地址是`C:\Program Files\MySQL\MySQL Server 5.7\lib`,如图：   
![链接器的修改](https://note.youdao.com/yws/api/personal/file/480A928A4A1741268CBFDA3951A67361?method=download&shareKey=db73e4d05ddc657db38a5217ae877f98)

4. 点击链接器中的输入，在附加依赖项中添加==libmysql.lib==，如图：   
![连接器输入修改](https://note.youdao.com/yws/api/personal/file/01BFC1E7BB674A97AD8523D24247C97C?method=download&shareKey=a9334efd4bc559efcba9f833314aef61)

5. 将mysql安装目录`C:\Program Files\MySQL\MySQL Server 5.7\lib`下的==libmysql.dll==复制到自己所建立的项目的**同名文件夹**下中,如图：
![dll文件](https://note.youdao.com/yws/api/personal/file/EFCCC934F2BA4C029E52E225E703E5DF?method=download&shareKey=88eaf808d942c86a7beca5fe15094b23)

6. 将运行的平台给为x64为，如图：
![修改平台环境](https://note.youdao.com/yws/api/personal/file/E6159B9DC60F4B04A3BD742802864824?method=download&shareKey=cdea8c714736ea54ab1cf8b66c7c48af)

### 三、数据库操作代码
>说明：这里我使用的是远程的数据库来进行连接
```c
#include <mysql.h>
#include <stdio.h>

int main()
{
	int res;
	MYSQL conn;
    //初始化MySQL连接句柄
	mysql_init(&conn);
	if (&conn != NULL)
	{
		printf("mysql句柄初始化成功\n");
	}
	else
	{
		printf("Err in init\n");
		return -1;
	}
	//连接mysql数据库
	if (mysql_real_connect
	    (&conn,  //MySQL句柄 
		"192.168.37.134",  //参数地址，本地数据库使用localhost
		"root", //数据库名
		"123456", //数据库密码
		"db_test", //数据库名
		0, //数据库端口，0表示默认(即3306)
		NULL, //如果unix_socket不是NULL，字符串指定套接字或应该被使用的命名管道。注意host参数决定连接的类型
		0)) //通常是0
	{                      
		      
		printf("数据库连接成功\n");
	}
	else
	{
		printf("数据库连接失败\n");
		mysql_close(&conn);  //关闭连接
		return -1;
	}
	//数据的插入
	res = mysql_query(&conn, "insert into testTB3 values(5,'aa')"); //MySQL句柄  SQL语句
	if (res == 0)
	{
		printf("插入成功\n");
	}
	else
	{
		printf("插入失败\n");
		mysql_close(&conn);
		return -1;
	}
	//数据的删除
	res = mysql_query(&conn, "delete from testTB3 where name='aa'");
	if (res == 0)
	{
		printf("删除成功\n");
	}
	else
	{
		printf("删除失败\n");
		mysql_close(&conn);
		return -1;
	}
	//数据的查询
	res = mysql_query(&conn, "select * from testTB3");
	if (res == 0)
	{
		printf("查询成功\n");
	}
	else
	{
		printf("查询失败\n");
		mysql_close(&conn);
		return -1;
	}
	//解析查询结果
	MYSQL_RES *res_ptr;//指向结果集索引的指针
	res_ptr = mysql_store_result(&conn);//检索完整的结果集当当前程序
	if (res_ptr != NULL)
	{
		//打印出结果集中一共有多少行记录
		unsigned long Row = mysql_num_rows(res_ptr);//结果集中的行数
		printf("有%lu行记录\n", Row);
	}
	else
	{
		printf("结果集操作保留出错\n");
		mysql_close(&conn);
		return -1;
	}
	//取出字段名
	MYSQL_FIELD *fd;
	int i = 0;
	while (fd = mysql_fetch_field(res_ptr))
	{
		printf("%s\t", fd->name);
		i++;
	}
	putchar('\n');
	//取出所有内容
	MYSQL_ROW sqlrow;
	int j;
	while (sqlrow = mysql_fetch_row(res_ptr))
	{
		//将每一行的内容分割成每一个记录
		for (j = 0; j < i; j++)
		{
			printf("%s\t", sqlrow[j]);
		}
		putchar('\n');
	}

	//释放结果集索引所在内存
	mysql_free_result(res_ptr);

	mysql_close(&conn);
	return 0;
}
```
运行结果，如图所示：
![MySQL C语言操作结果](https://note.youdao.com/yws/api/personal/file/CA62786BA71D487393252F540A701279?method=download&shareKey=01ca503b6fc3d590541d1099de90c19b)

