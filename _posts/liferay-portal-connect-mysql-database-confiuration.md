title: Liferay Portal连接mysql数据库配置
date: 2014-03-30 21:52:55
categories: liferay
tags: [liferay, mysql]
description: Liferay Portal连接mysql数据库配置
keywords: liferay, mysql
---
本文将介绍Liferay Portal连接mysql数据库的相关配置。

### 开发环境
* OS：ubuntu 12.04 64位
* Liferay Portal：6.2.0-ce-ga1
* Mysql：5.5.35

### 创建Mysql用户及数据库
以root权限登录mysql，执行以下命令创建用户`lp62`、数据库`lportal`，并分配`lportal`的所有权限给`lp62`。
``` mysql
create user 'lp62'@'localhost' identified by 'lp62';
create database lportal character set utf8;
grant all privileges on lportal.* to 'lp62'@'localhost';
flush privileges;
```
<!-- more -->
### 创建portal-ext.properties文件并添加配置
在`LP_HOME`下创建`portal-ext.properties`文件。此时`LP_HOME`下的目录结构如下：
``` bash
.
├── data
├── license
├── portal-ext.properties
├── readme.html
└── tomcat-7.0.42
```
添加以下配置到`portal-ext.properties`。
``` bash
jdbc.default.driverClassName=com.mysql.jdbc.Driver
jdbc.default.url=jdbc:mysql://localhost/lportal?useUnicode=true&characterEncoding=UTF-8&useFastDateParsing=false
jdbc.default.username=lp62
jdbc.default.password=lp62
```

### 启动Liferay Portal
切换目录到`LP_HOME/tomcat-7.0.42/bin`目录下，执行`./startup.sh`。查看`LP_HOME/tomcat-7.0.42/log/catalina.out`，日志中包含以下一条，说明Liferay Portal正在初始化数据。
```
14:30:24,670 INFO  [localhost-startStop-1][ReleaseLocalServiceImpl:84] Create tables and populate with default data
```
由于需要创建表和初始数据，所以第一次执行需要较长时间，之后启动时则不需要。几分钟后，日志中出现
```
信息: Server startup in 486616 ms
```
说明启动成功。默认浏览器会打开`http://localhost:8080/`页面。之后再选择默认语言，创建模拟数据，输入密码提示等操作。就可以使用以Mysql为数据库的Liferay Portal了。

---
全文完