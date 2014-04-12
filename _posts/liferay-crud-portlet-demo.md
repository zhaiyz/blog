title: Liferay crud portlet demo
date: 2014-04-05 20:51:32
categories: liferay
tags: [liferay, portlet]
description: Liferay crud portlet demo
keywords: liferay, portlet
---
本文将介绍如果创建一个拥有CRUD功能的portlet。项目代码已托管到github，地址为：https://github.com/zhaiyz/sample-portlet 可使用以下命令下载代码：
``` bash
git clone https://github.com/zhaiyz/sample-portlet.git sample
```

### 开发环境
* OS：ubuntu 12.04 64位
* JDK：1.6.0_45
* Maven：3.0.5
* Liferay Portal：6.2.0-ce-ga1
* Struts2：2.3.16.1

### 开发过程
1. 创建一个`sample`portlet，参考[Liferay Service Builder](http://zhaiyz.com/2014/04/01/liferay-service-builder/)
2. 集成struts，参考[Liferay集成Struts2](http://zhaiyz.com/2014/03/31/develop-lifeay-portlet-with-struts2/)
3. 创建数据库表结构，参考[Liferay Service Builder](http://zhaiyz.com/2014/04/01/liferay-service-builder/)
4. 创建自定义方法，参考[Liferay添加自定义服务层方法](http://zhaiyz.com/2014/04/02/add-methods-to-service-impl/)
5. 创建应用层类，包含`BookListAction`、`BookAddAction`、`BookDeleteAction`、`BookEditAction`
6. 创建显示层页面，包含`view.jsp`、`edit.jsp`
7. 创建`struts.xml`，并配置`action`与`jsp`的关联

---
未完待续