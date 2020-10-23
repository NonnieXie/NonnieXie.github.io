---
title: 02_Qt常用的控件_QLineEdit(单行文本编辑器)
tags: [Qt]
categories: Qt
---
## 一、QLineEdit
QlineEdit为Qt的单行文本编辑器。
### 1.1、设置获取内容
- 获取编辑器框内容使用text()
```
QString str =ui->lineEdit->text();
qDebug()<<str;
```
- 设置编辑框内容使用setText()
```
 ui->lineEdit->setText("123");
```
### 1.2、设置内容显示的间隔
我们在使用QLineEdit显示文本的时候，希望在左侧流出一些空白位置，这个时候就需要我们使用QLineEdit提供的setTextMargins函数：    
函数声明：`void QLineEdit::setTextMargins(int left, int top, int right, int bottom)`   
此函数可以指定显示的文本与输入框上下左右边界的像素数
```
ui->lineEdit->setTextMargins(15,0,0,0); //这里的间距是以像素点为单位
```
### 1.3、设置显示的模式
我们使用QLineEdit类的setEchoMode()函数来进行设置文本的显示模式，函数的声明：
`void setEchoMode(EchoMode)`
EchoMode是一个枚举类型,一共定义了四种显示模式:       
- QLineEdit::Normal	 模式显示方式，按照输入的内容显示。        
- QLineEdit::NoEcho	不显示任何内容，此模式下无法看到用户的输入。       
- QLineEdit::Password	密码模式，输入的字符会根据平台转换为特殊字符。  
- QLineEdit::PasswordEchoOnEdit	编辑时显示字符否则显示字符作为密码。    
```
ui->lineEdit->setEchoMode(QLineEdit::Password); 
```  
### 1.4、设置输入提示
我们想输入一个或者几个字符，下边就会列出和我们输出的字符相匹配的字符串，QLineEdit要实现这样的功能可以使用该类的成员函数setComleter()函数来实现:
`void QLineEdit::setCompleter(QCompleter *c) `   
```
QStringList list; //需要#include <QStringList> 字符串链表头文件
list<<"Hello"<<"How are you!"<<"hehe";
QCompleter *com = new QCompleter(list,this);  //需要#include <QCompleter>
com->setCaseSensitivity(Qt::CaseInsensitive);
ui->lineEdit->setCompleter(com);
```
QCompleter类的setCaseSensitivity()函数可以设置是否区分大小写，它的参数是一个枚举类型：    
- Qt::CaseInsensitive	不区分大小写         
- Qt::CaseSensitive    区分大小写  

如果不设置该属性，默认匹配字符串时是区分大小写的。              