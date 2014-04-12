title: "Apache ActiveMQ的安装与启动"
id: 199
date: 2013-07-30 20:40:08
tags: 
- activemq
- jms
categories: 
- activemq
---

Apache ActiveMQ是一个开源的消息中间件。下面介绍一下它的安装与启动。

1.  下载地址：http://activemq.apache.org/download.html
2.  下载完成后解压，假设解压到的目录为%ACTIVEMQ_HOME%
3.  命令行下切换到%ACTIVEMQ_HOME%/bin目录
4.  启动Active MQ：windows下执行activemq，linux下执行./activemq start
5.  访问http://localhost:8161，用户名：admin，密码：admin
6.  代码是向Apache ActiveMQ发送消息的地址是tcp://localhost:61616
7.  停止Active MQ：windows下使用Ctrl+C，linux下执行./activemq stop