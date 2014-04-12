title: "mysql创建数据库及用户"
id: 159
date: 2013-03-07 22:55:52
tags: 
- mysql
categories: 
- mysql
---

``` mysql
create database liferay character set utf8;
create user 'liferay'@'%' identified by 'liferay';
grant all privileges on liferay.* to 'liferay'@'%';
```