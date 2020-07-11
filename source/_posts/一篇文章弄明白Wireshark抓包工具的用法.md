---
title: 一篇文章弄明白Wireshark抓包工具的用法
tags: [开发工具]
categories: 开发工具
top: true
---
#  wireshark网络抓包工具
Wireshark（前称Ethereal）是一个网络封包分析软件。网络封包分析软件的功能是撷取网络封包，并尽可能显示出最为详细的网络封包资料。Wireshark使用WinPCAP作为接口，直接与网卡进行数据报文交换。
网络封包分析软件的功能可想像成 "电工技师使用电表来量测电流、电压、电阻" 的工作 - 只是将场景移植到网络上，并将电线替换成网络线。

wireshark的官方下载地址：[https://www.wireshark.org/download.html](https://www.wireshark.org/download.html)

wireshark是非常流行的网络封包分析软件，功能十分强大。可以截取各种网络封包，从而显示网络封包的详细信息。

### Wireshark不能做
wireshark不能够修改封包的内容或者发送封包，只能够只来查看封包。
### wireshark开始进行抓包
#### wireshark开始界面
wiershark是用来捕捉电脑上的某一个网卡的网络包，而电脑上具有多个网卡的时候就需要进行从着多个网卡中选择，你需要的一个网卡。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200328010213635.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjMwODEw,size_16,color_FFFFFF,t_70)

#### wireshark窗口介绍
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200328010233901.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjMwODEw,size_16,color_FFFFFF,t_70)
WireShark 主要分为这几个界面
1. Display Filter(显示过滤器)，  用于过滤
2. Packet List Pane(封包列表)， 显示捕获到的封包， 有源地址和目标地址，端口号。 颜色不同，代表
3. Packet Details Pane(封包详细信息), 显示封包中的字段
4. Dissector Pane(16进制数据)
5. Miscellanous(地址栏，杂项)

#### wireshark显示过滤
使用显示过滤的原因，在我们者初次使用wireshark时，将会产生大量的冗余数据，想想这么多的数据让我们在其中找到我们需要的部分，这样就显得非常的难。
相对而言过滤器就会在大量的数据中能够让我们从中找到我们所需要的数据信息。
过滤器有两种：
1. 显示过滤器，就是主界面上那个，用于在捕获的记录中找到所需要的记录
2. 捕获过滤器：用来过滤捕获的封 包，以避免捕获的太多记录。在捕获→捕获过滤器
#### 过滤表达式的规则
1. 协议过滤
`TCP`	只显示TCP协议。
2. IP 过滤
```bash
ip.src ==192.168.1.102				显示源地址为192.168.1.102
ip.dst==192.168.1.102				目标地址为192.168.1.102
```
3. 端口过滤
```
	tcp.port == 80				端口为80的       
	tcp.srcport == 80			只显示TCP协议的愿端口为80的。
```
	
4. Http模式过滤
```
http.request.method=="GET"		只显示HTTP GET方法的。
request.method=="GET"			只显示HTTP GET方法的。
```
5. 逻辑运算符为 AND/ OR

[^1]:我的
