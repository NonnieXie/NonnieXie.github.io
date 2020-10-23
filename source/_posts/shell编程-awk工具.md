---
title: awk文本分析工具
tags: [shell]
categories: shell
---
### 一、awk工具
`sed`是以行为单位处理文件，`awk`比`sed`强的地方在于不仅可以使用行为单位也可以使用列为单位处理文件。awk缺省的行分隔符是换行，缺省的列分隔符是连续的空格和tab,但是行分隔和列分隔符都可以进行自定义。比如`/etc/passwd`文件的每一行有若干个字段，字段之间以:分隔，就可以重新定义`awk`的列分隔符为:并以列为单位处理这个文件。

`awk`的基本用法和`sed`类似，`awk`命令行的基本的形式：
```
awk 参数 '脚本语句(/pattern/{actions})' 待操作文件
awk 参数 -f '脚本文件'  待操作文件
```
>注意：`printf`不带换行，`print`带换行

例如：
```
awk '{print $0}' awk.sh  #打印整个文件
awk '{print $1}' awk.sh #打印每一行的的第一列
awk '/^ *$/{count=count+1} END {print count}' test.txt  #统计一个文件中的空行
ps aux | awk '{print $2}' #打印进程的PID
ps aux | awk '$2>20000 {print $2}' #打印PID大于20000的
ps aux | awk '$2>2000 && $2<=3000 {count=count+1} END {print count}'  #统计PID大于2000小于3000的个数

```
awk常用的内建变量：
| 变量| 变量说明|
|---|---|
|FILENAME|当前输入文件的文件名，该变量只读的|
|FILENAME|当前输入文件的文件名，该变量是只读的
|NR 	|当前行的行号，该变量是只读的，R代表record
|NF 	|当前行所拥有的列数，该变量是只读的，F代表field
|OFS 	|输出格式的列分隔符，缺省是空格
|FS 	|输入文件的列分融符，缺省是连续的空格和Tab
|ORS 	|输出格式的行分隔符，缺省是换行符
|RS 	|输入文件的行分隔符，缺省是换行符

例如打印系统中的用户账号列表：
```
awk -F: '{print $1}' /etc/passwd  #自定义:为分隔符，打印/etc/passwd的第一列
 awk 'BEIN {FS=":"} {print $1;}' /etc/passwd
```

`awk`还可以想c语言一样使用`if/else、while、for`控制结构。可自行自行学习。

