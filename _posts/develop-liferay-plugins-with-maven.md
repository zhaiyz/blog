title: Liferay Portal Maven开发环境搭建
date: 2014-03-29 13:55:26
categories: [liferay]
tags: [liferay, maven, portlet]
description: Liferay Portal Plugins Maven开发环境搭建
keywords: liferay, maven, portlet
---
本文将介绍从lifeay portal下载，创建maven项目到发布portlet的全过程。

### 开发环境
* OS：ubuntu 12.04 64位
* JDK：1.6.0_45
* Maven：3.0.5
* Liferay Portal：6.2.0-ce-ga1

### 下载Lifeay Portal
* 百度网盘下载链接：http://pan.baidu.com/s/1ntoHVfF
* 官方下载链接：http://jaist.dl.sourceforge.net/project/lportal/Liferay%20Portal/6.2.0%20GA1/liferay-portal-tomcat-6.2.0-ce-ga1-20131101192857659.zip

### 解压Liferay Portal
把上一步下载的文件解压，得到`liferay-portal-6.2.0-ce-ga1`文件夹。把此文件夹copy至自己喜欢的一个目录，定义`tomcat-7.0.42`所在目录为`LP_HOME`，此时`LP_HOME`的目录结构如下：
``` bash
.
├── data
├── license
├── readme.html
└── tomcat-7.0.42
```
<!-- more -->
### 创建Maven项目
由于6.2.0-ce-ga1版本的liferay portal还没有在maven中央库，需要使用liferay官方的库，地址为：https://repository.liferay.com/nexus/content/groups/liferay-ce
现在使用如下命令创建一个名为`sample-portlet`的项目：
``` bash
mvn archetype:generate \
    -DarchetypeArtifactId=liferay-portlet-archetype \
    -DarchetypeCatalog=https://repository.liferay.com/nexus/content/groups/liferay-ce/archetype-catalog.xml \
    -DarchetypeGroupId=com.liferay.maven.archetypes \
    -DarchetypeRepository=https://repository.liferay.com/nexus/content/groups/liferay-ce \
    -DarchetypeVersion=6.2.0-ga1 \
    -DgroupId=com.zhaiyz \
    -DartifactId=sample-portlet \
    -DinteractiveMode=false
```
创建的项目目录如下：
``` bash
sample-portlet/
├── pom.xml
└── src
    └── main
        ├── java
        ├── resources
        └── webapp
            ├── css
            │   └── main.css
            ├── icon.png
            ├── js
            │   └── main.js
            ├── view.jsp
            └── WEB-INF
                ├── liferay-display.xml
                ├── liferay-plugin-package.properties
                ├── liferay-portlet.xml
                ├── portlet.xml
                └── web.xml
```
因为此时的pom.xml中的变量都还未赋值，而且需要把依赖库和插件库指向liferay官方库，所以要在pom.xml文件中添加如下配置：
``` xml
<project ...>
	.
    .
    .
	<properties>
    	<!-- 指向自己的LP_HOME -->
		<liferay.home>/home/zhaiyz/develop/liferay-portal-6.2.0-ce-ga1</liferay.home>
		<liferay.auto.deploy.dir>${liferay.home}/deploy</liferay.auto.deploy.dir>
		<liferay.app.server.deploy.dir>${liferay.home}/tomcat-7.0.42/webapps</liferay.app.server.deploy.dir>
		<liferay.app.server.lib.global.dir>${liferay.home}/tomcat-7.0.42/lib/ext</liferay.app.server.lib.global.dir>
		<liferay.app.server.portal.dir>${liferay.home}/tomcat-7.0.42/webapps/ROOT</liferay.app.server.portal.dir>
		<liferay.version>6.2.0-ga1</liferay.version>
		<liferay.maven.plugin.version>6.2.0-ga1</liferay.maven.plugin.version>
	</properties>
    .
    .
    .
    <pluginRepositories>
		<pluginRepository>
			<id>liferay-plugin-repo</id>
			<name>Liferay Repo</name>
			<url>https://repository.liferay.com/nexus/content/groups/liferay-ce/</url>
			<layout>default</layout>
			<snapshots>
				<enabled>false</enabled>
			</snapshots>
			<releases>
				<updatePolicy>never</updatePolicy>
			</releases>
		</pluginRepository>
	</pluginRepositories>
	<repositories>
		<repository>
			<id>liferay-repo</id>
			<name>Liferay Repo</name>
			<url>https://repository.liferay.com/nexus/content/groups/liferay-ce/</url>
		</repository>
	</repositories>
    .
    .
    .
</project>
```
运行以下命令进行打包
``` bash
mvn package
```
此时在sample-portlet/target目录下就会生成`sample-portlet-1.0-SNAPSHOT.war`，再执行以下命令，就可以把生成的war包发布至`LP_HOME`的deploy目录下
``` bash
mvn liferay:deploy
```
启动`LP_HOME`下的tomcat，即可部署刚创建的portlet。

---
全文完