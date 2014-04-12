title: 使用eclipse开发liferay maven项目
date: 2014-04-11 23:01:46
categories: liferay
tags: [liferay, eclipse, maven]
description: 使用eclipse开发liferay maven项目
keywords: liferay, eclipse, maven
---
本文将介绍使用eclipse开发liferay maven项目。

> 之前用sublime text写过一些liferay代码，但是很不方便，主要是进行包引入时和使用方法进行提示时。所以以后还是使用eclipse进行开发。

### 开发环境
* OS：ubuntu 12.04 64位
* Liferay Portal：6.2 CE GA2(6.2.1)
* JDK：1.6.0_45
* Maven：3.0.5
* Eclipse：3.7.2(indigo)

### 创建maven项目
> liferay 6.2.1相关的archetypes已经在4月2号更新到了maven中央库，所以如果平时把maven启动时更新库索引的选项去掉的话，需要选上[如下图]再重启eclipse，这样就可以更新最到新的索引。

<!-- more -->
![maven_preferences](http://zhaiyz.qiniudn.com/images/blog/20140411/maven_preferences.png)
完成以上操作后在eclipse中新建一个maven project，在`Select an Archetype`页面的Filter中输入`liferay`即可检索出liferay相关的archtypes。但是在我本机，虽然更新到了最新的索引，看到的最新的liferay archtypes的版本却是`6.2.0-M6`。

![maven_liferay_archtypes](http://zhaiyz.qiniudn.com/images/blog/20140411/maven_liferay_archtypes.png)

#### 添加liferay私有Catalog
为了使用最新的archtype，需要添加liferay官网提供的catalog。方法如下，在上图中点击`Configure`按钮，或选择Window->Preferences->Maven->Archtypes。再点击`Add Remote Catalog`按钮。在弹出的对话框中。添加`https://repository.liferay.com/nexus/content/groups/liferay-ce/archetype-catalog.xml`到`Catelog File`栏中，`Description`可以自定义，本机使用`liferay-ce-archtype-catalog`[如下图]。填写完成后，点击OK按钮保存。

![maven_archtypes_liferay_catalog](http://zhaiyz.qiniudn.com/images/blog/20140411/maven_archtypes_liferay_catalog.png)

#### 创建liferay项目
重新回到创建maven项目界面，Catelog下拉框中选择刚添加的`liferay-ce-archtype-catalog`，Fileter输入`liferay`，同时还需要把`Show the last version of Archtype only`选项去掉，不然的话，只会显示最新的版本。在列出的可先archtype中，选择Artifact Id为`liferay-portlet-archtype`，Version选择`6.2.1`[如下图]。

![maven_archtypes_liferay_6.2.1](http://zhaiyz.qiniudn.com/images/blog/20140411/maven_archtypes_liferay_6.2.1.png)

完成以上操作之后，点击Next按钮进入`Specify Archetype parameters`界面。根据需求，添加好Group Id，Artifact Id等信息，本文使用配置[如下图]。

![maven_liferay_demo](http://zhaiyz.qiniudn.com/images/blog/20140411/maven_liferay_demo.png)

填写好配置之后，点击Finish，eclipse就会根据选定的archtype和配置创建好一个项目。项目目录结构如下，其中target目录是自动出成的：
``` bash
.
├── pom.xml
├── src
│   ├── main
│   │   ├── java
│   │   ├── resources
│   │   └── webapp
│   │       ├── css
│   │       │   └── main.css
│   │       ├── icon.png
│   │       ├── js
│   │       │   └── main.js
│   │       ├── view.jsp
│   │       └── WEB-INF
│   │           ├── liferay-display.xml
│   │           ├── liferay-plugin-package.properties
│   │           ├── liferay-portlet.xml
│   │           ├── portlet.xml
│   │           └── web.xml
│   └── test
│       └── java
└── target
    ├── classes
    ├── m2e-wtp
    │   └── web-resources
    │       └── META-INF
    │           └── maven
    │               └── com.zhaiyz
    │                   └── demo
    │                       ├── pom.properties
    │                       └── pom.xml
    └── test-classes

19 directories, 12 files
```

#### 配置pom.xml
添加以下配置到pom.xml中，主要是指定项目中的使用liferay及liferay maven plugin版本，liferay运行环境的相关路径，以及把库和插件库指向liferay官网。
``` xml
<properties>
    <!-- 指向自己的LP_HOME -->
    <liferay.home>/home/zhaiyz/develop/liferay-portal-6.2.0-ce-ga1</liferay.home>
    <liferay.auto.deploy.dir>${liferay.home}/deploy</liferay.auto.deploy.dir>
    <liferay.app.server.deploy.dir>${liferay.home}/tomcat-7.0.42/webapps</liferay.app.server.deploy.dir>
    <liferay.app.server.lib.global.dir>${liferay.home}/tomcat-7.0.42/lib/ext</liferay.app.server.lib.global.dir>
    <liferay.app.server.portal.dir>${liferay.home}/tomcat-7.0.42/webapps/ROOT</liferay.app.server.portal.dir>
    <liferay.version>6.2.1</liferay.version>
    <liferay.maven.plugin.version>6.2.1</liferay.maven.plugin.version>
</properties>

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
```
完成以上配置之后，再在项目文件夹上点击右键，选择Maven->Update Project...。这样eclipse就会下载下项目需要的依赖。再在项目中运行以下命令，即可打包、发布项目。也可以使用项目右键中Run As中的maven相关命令运行。
``` bash
mvn clean package liferay:deploy
```
--**EOF**--

