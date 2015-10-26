title: 使用springmvc开发portlet
date: 2014-04-21 22:47:44
categories: liferay
tags: [liferay, portlet, springmvc]
description: 使用springmvc开发portlet
keywords: liferay, portlet, springmvc
---
> 本文将介绍使用springmvc开发一个portlet。项目全部代码已托管在github，地址为：https://github.com/zhaiyz/springmvc-portlet

### 开发环境
* OS：ubuntu 12.04 64位
* Liferay Portal：6.2 CE GA2(6.2.1)
* JDK：1.6.0_45
* Maven：3.0.5
* Eclipse：3.7.2(indigo)
* Spring：3.2.4.RELEASE

### 创建一个portlet
依照[使用eclipse开发liferay maven项目](http://zhaiyz.com/2014/04/11/use-eclipse-develop-liferay-with-maven/)中的方法，创建一个名为`springmvc-portlet`的portlet。

### 添加springmvc-portlet依赖
在`pom.xml`中添加`spring-webmvc-portlet`依赖，以及`jstl`依赖。
``` xml
<project>
    ...
    <dependencies>
    	<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-webmvc-portlet</artifactId>
			<version>3.2.4.RELEASE</version>
		</dependency>
		<dependency>
			<groupId>javax.servlet</groupId>
			<artifactId>jstl</artifactId>
			<version>1.2</version>
		</dependency>
    </dependencies>
    ...
    
</project>
```
<!-- more -->
### 添加web.xml配置
``` xml
<?xml version="1.0"?>

<web-app version="2.4" xmlns="http://java.sun.com/xml/ns/j2ee"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://java.sun.com/xml/ns/j2ee http://java.sun.com/xml/ns/j2ee/web-app_2_4.xsd">
	<servlet>
		<servlet-name>ViewRendererServlet</servlet-name>
		<servlet-class>org.springframework.web.servlet.ViewRendererServlet</servlet-class>
	</servlet>
	<servlet-mapping>
		<servlet-name>ViewRendererServlet</servlet-name>
		<url-pattern>/WEB-INF/servlet/view</url-pattern>
	</servlet-mapping>
</web-app>
```

### 创建`SpringMvcPortletController`
``` java
package com.zhaiyz;

import javax.portlet.RenderRequest;
import javax.portlet.RenderResponse;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.portlet.bind.annotation.RenderMapping;

/**
 * SpringMvcPortletController
 * 
 * @author zhaiyz
 */
@Controller
@RequestMapping(value = "VIEW")
public class SpringMvcPortletController {

    @RenderMapping
    public String showForm(RenderRequest request, RenderResponse response) throws Exception {
        return "view";
    }
}
```

### 创建springmvc-portlet.xml
``` xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:context="http://www.springframework.org/schema/context"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://www.springframework.org/schema/beans
		http://www.springframework.org/schema/beans/spring-beans-3.2.xsd
		http://www.springframework.org/schema/context
		http://www.springframework.org/schema/context/spring-context-3.2.xsd">

	<context:component-scan base-package="com.zhaiyz" />  
	
	<bean id="viewResolver" class="org.springframework.web.servlet.view.InternalResourceViewResolver">
		<property name="viewClass" value="org.springframework.web.servlet.view.JstlView" />
		<property name="prefix" value="/WEB-INF/jsp/" />
		<property name="suffix" value=".jsp" />
	</bean>
</beans>
```

### 修改portlet.xml
``` xml
<?xml version="1.0"?>

<portlet-app xmlns="http://java.sun.com/xml/ns/portlet/portlet-app_2_0.xsd"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://java.sun.com/xml/ns/portlet/portlet-app_2_0.xsd http://java.sun.com/xml/ns/portlet/portlet-app_2_0.xsd"
	version="2.0">
	<portlet>
		<portlet-name>springmvc-portlet</portlet-name>
		<display-name>springmvc-portlet</display-name>
		<portlet-class>org.springframework.web.portlet.DispatcherPortlet</portlet-class>
		<init-param>
			<name>contextConfigLocation</name>
			<value>classpath:springmvc-portlet.xml</value>
		</init-param>
		<expiration-cache>0</expiration-cache>
		.
        .
        .
	</portlet>
</portlet-app>
```

### 创建jsp目录及view.jsp文件
在`WEB-INF`下创建`jsp`目录，并把自动创建的在`webapp`目录下的`view.jsp`移动到`jsp`目录。此时，项目的目录结构如下：
``` bash
.
├── pom.xml
└── src
    └── main
        ├── java
        │   └── com
        │       └── zhaiyz
        │           └── SpringMvcPortletController.java
        ├── resources
        │   └── springmvc-portlet.xml
        └── webapp
            ├── css
            │   └── main.css
            ├── icon.png
            ├── js
            │   └── main.js
            └── WEB-INF
                ├── jsp
                │   └── view.jsp
                ├── liferay-display.xml
                ├── liferay-plugin-package.properties
                ├── liferay-portlet.xml
                ├── portlet.xml
                └── web.xml

11 directories, 12 files
```

### 打包发布
``` bash
mvn clean pakcage liferay:deploy
```
启动tomcat，启动完成后。可应用程序的示例分类中找到新创建的portlet，名为`springmvc-portlet`。添加此portlet到页面，可以看到如下显示效果。
![springmvc_portlet](http://zhaiyz.qiniudn.com/images/blog/20140421/springmvc_portlet.png)

### 参考文献
1. [Development of a Simple Portlet with SpringMVC](http://blogs.isostech.com/portlet-development/development-simple-portlet-spring-mvc/)
2. [Liferay 6.1开发学习（十七）：基于注解的SpringMVC portlet开发](http://www.huqiwen.com/2013/01/10/liferay-6-1-development-study-17-springmvc-portlet/)
3. [java.lang.ClassNotFoundException : javax.servlet.jsp.jstl.core.Config](http://www.mkyong.com/jsf2/java-lang-classnotfoundexception-javax-servlet-jsp-jstl-core-config/)

--**EOF**--