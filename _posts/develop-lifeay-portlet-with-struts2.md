title: Liferay集成Struts2
date: 2014-03-31 20:22:39
categories: [liferay]
tags: [liferay, struts, portlet]
description: Liferay集成Struts2
keywords: liferay, maven, portlet
---
本文将介绍使用struts2开发Liferay Portal。

### 开发环境
* OS：ubuntu 12.04 64位
* Liferay Portal：6.2.0-ce-ga1
* Struts2：2.3.16.1

### 创建portlet
使用[Liferay Portal Maven开发环境搭建](http://zhaiyz.com/2014/03/29/develop-liferay-plugins-with-maven/)文章中的步骤，创建一个`sample-portlet`项目。

### 集成struts2
在`pom.xml`中添加struts2-portlet-plugin依赖
``` xml
<dependency>
	<groupId>org.apache.struts</groupId>
    <artifactId>struts2-portlet-plugin</artifactId>
    <version>2.3.16.1</version>
</dependency>
```
<!-- more -->
在`sample-portlet/src/main/resources`目录下创建`struts.xml`文件，并添加以下内容。此项目不需要自己编写action类，使用struts自带的即可。
``` xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE struts PUBLIC
	"-//Apache Software Foundation//DTD Struts Configuration 2.3//EN"
	"http://struts.apache.org/dtds/struts-2.3.dtd">

<struts>
    <package name="sample-portlet" namespace="/sample-portlet" extends="struts-portlet-default">
        <action name="view" class="com.opensymphony.xwork2.ActionSupport">
            <result name="success">/WEB-INF/jsp/view.jsp</result>
        </action>
    </package>
</struts>
```
在`WEB-INF`目录下创建`jsp`文件夹，并把在`webapp`目录下的`view.jsp`移动到`jsp`目录。现在项目的目录结构如下：
``` bash
.
├── pom.xml
├── src
│   └── main
│       ├── java
│       ├── resources
│       │   └── struts.xml
│       └── webapp
│           ├── css
│           │   └── main.css
│           ├── icon.png
│           ├── js
│           │   └── main.js
│           └── WEB-INF
│               ├── jsp
│               │   └── view.jsp
│               ├── liferay-display.xml
│               ├── liferay-plugin-package.properties
│               ├── liferay-portlet.xml
│               ├── portlet.xml
│               └── web.xml
```

修改`portlet.xml`中的内容以集成struts2，主要是使用`org.apache.struts2.portlet.dispatcher.Jsr286Dispatcher`替换`com.liferay.util.bridges.mvc.MVCPortlet`，再添加portlet需要运行action所在的namespace和默认执行的action名称等配置参数。
``` xml
<?xml version="1.0"?>

<portlet-app ...>
	<portlet>
		<portlet-name>sample-portlet</portlet-name>
		<display-name>sample-portlet</display-name>
		<portlet-class>org.apache.struts2.portlet.dispatcher.Jsr286Dispatcher</portlet-class>
		<init-param>
            <!-- 对应struts.xml中package的namespace -->
			<name>portletNamespace</name>
			<value>/sample-portlet</value>
		</init-param>
		<init-param>
            <!-- 对应struts.xml中action的name -->
			<name>defaultViewAction</name>
			<value>view</value>
		</init-param>
		<expiration-cache>0</expiration-cache>
		.
        .
        .
	</portlet>
</portlet-app>
```

### 编译打包并发布
在`sample-portlet`目录下执行以下命令，如果之前没有下载过相关依赖，那么第一次运行时会下载所有依赖。
``` bash
mvn clean package liferay:deploy
```
启动liferay portal的tomcat。启动完毕后，以管理员身份登录，添加应用程序，在示例分类下可以找到`sample-portlet`，添加至页面，即可显示。

---
全文完