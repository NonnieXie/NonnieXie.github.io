---
title: sed流编译器
tags: [shell]
categories: shell
---
### 一、sed工具
`sed`为流编译器，是对一个文档中的行数据进行处理。我们都知道，`sed`和`vi`都是早期的UNIX的工具，因此很多的`sed`命令和`vi`的末行命令都是非常相似的。
     
如果将`test.sh`中的`echo`替换为`printf`
- 可以使用`vim编译器`的末行模式输入`:%s/echo/printf/g`。而在命令模式输入`uu`来进行撤销。
- 也可以使用`sed流编译器`来进行修改。   

`sed`命令的基本格式：
```
sed 参数 `'脚本语句(/pattern/{actions})'` 待操控文件    
sed 参数 -f `脚本文件` 待操控的文件
```
---

有关`sed`的选项含义：
```
--version 				显示sed版本。
--help					显示帮助文档。
-n,--quiet,--silent 	静默输出，默认情况下，sed程序在所有的脚本指令执行完毕后，将自动打印模式空间中的内容，这些选项可以屏蔽自动打印。
-e script 				允许多个脚本指令被执行。
-f script-file,
--file=script-file 		从文件中读取脚本指令，对编写自动脚本程序来说很棒！
-i,--in-place 			直接修改源文件，经过脚本指令处理后的内容将被输出至源文件（源文件被修改）慎用！
-l N, --line-length=N 	该选项指定l指令可以输出的行长度，l指令用于输出非打印字符。
--posix 				禁用GNU sed扩展功能。
-r, --regexp-extended 	在脚本指令中使用扩展正则表达式
-s, --separate 			默认情况下，sed将把命令行指定的多个文件名作为一个长的连续的输入流。而GNU sed则允许把他们当作单独的文件，这样如正则表达式则不进行跨文件匹配。
-u, --unbuffered 		最低限度的缓存输入与输出。
```
-----

上面的是sed本身选项功能说明，这里介绍几个常用简单的sed操作。

|简称|原名|汉语意思|
|---|---|---
|a|	append| 追加
|i|	insert |插入
|d|	delete 	|删除
|s|	substitution |替换

例如：
```
sed '4a hello' case.sh  #在case.sh文件的第四行添加hello
sed '5d' test.sh  #删除test.sh的第五行数据
sed '2,5d' test.sh #删除test.sh的第二行到第五行数据
sed 's/echo/printf/g' test.sh #将test.sh中的echo替换为printf 
```
#### 1.1、常用的sed命令
`sed`的编辑命令可以直接当命令行参数传入，也可以写成一个脚本文件然后用`-f`参数指定，编辑命令的格式为：
`/pattern/action`
>说明：其中pattern是正则表达式，action是编辑操作。sed程序一行一行读出待处理文件，如果某一行与pattern匹配，则执行相应的action，如果一条命令没有pattern而只有action，这个action将作用于待处理文件的每一行。

```
/pattern/p  #打印匹配pattern的行
/pattern/d  #删除匹配pattern的行
/pattern/s/pattern1/pattern2/ #查找符合pattern的行，将该行第一个匹配pattern1的字符串替换为pattern2
/pattern/s/pattern1/pattern2/g #查找符合pattern的行，将该行所有匹配pattern1的字符串替换为pattern2
```
在使用p命令的时候，要注意p命令表示除了把文件内容打印出来之外还额外打印一遍匹配pattern的行。如果我们就想要输出结果，可以加上`-n`选项
```
sed '/echo/p' test.sh
sed '/echo/d' test.sh
sed '/echo/echo~~/' test.sh
sed '/echo~~/echo/g' test.sh
sed 's/<.*>//g'  test.html  #去掉所有的html标签
```

