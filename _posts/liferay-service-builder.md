title: Liferay Service Builder
date: 2014-04-01 21:34:15
categories: liferay
tags: [liferay, service]
description: Liferay Service Builder
keywords: liferay, service bulder 
---
本文将介绍`service.xml`文件的配置，定义一个实体并执行`mvn liferay:build-service`创建出数据库脚本及相关的`model`、`service`等文件。

### 开发环境
* OS：ubuntu 12.04 64位
* Liferay Portal：6.2.0-ce-ga1
* Mysql：5.5.35

### 创建portlet
使用以下命令创建名为`sample`的项目。其中`archetypeArtifactId`为`liferay-servicebuilder-archetype`。
``` bash
mvn archetype:generate \
    -DarchetypeArtifactId=liferay-servicebuilder-archetype \
    -DarchetypeCatalog=https://repository.liferay.com/nexus/content/groups/liferay-ce/archetype-catalog.xml \
    -DarchetypeGroupId=com.liferay.maven.archetypes \
    -DarchetypeRepository=https://repository.liferay.com/nexus/content/groups/liferay-ce \
    -DarchetypeVersion=6.2.0-ga1 \
    -DgroupId=com.zhaiyz \
    -DartifactId=sample \
    -DinteractiveMode=false
```
<!-- more -->
运行完成之后，项目目录如下：
``` bash
sample/
├── pom.xml
├── sample-portlet
│   ├── pom.xml
│   └── src
│       └── main
│           ├── java
│           ├── resources
│           │   └── portlet.properties
│           └── webapp
│               ├── css
│               │   └── main.css
│               ├── icon.png
│               ├── js
│               │   └── main.js
│               ├── view.jsp
│               └── WEB-INF
│                   ├── liferay-display.xml
│                   ├── liferay-plugin-package.properties
│                   ├── liferay-portlet.xml
│                   ├── portlet.xml
│                   ├── service.xml
│                   └── web.xml
└── sample-portlet-service
    └── pom.xml
```

其中`sample`为父项目，`sample-portlet`和`sample-portlet-service`为子项目。修改`sample/pom.xml`文件，添加以下内容：
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
两个子项目中不需要添加此配置，可以直接继承父项目的属性。

### 配置service.xml文件，并生成相关代码
修改`service.xml`文件中的内容为以下配置：
``` xml
<!DOCTYPE service-builder PUBLIC "-//Liferay//DTD Service Builder 6.2.0//EN" "http://www.liferay.com/dtd/liferay-service-builder_6_2_0.dtd">

<service-builder package-path="com.zhaiyz">
    <author>zhaiyz</author>
    <namespace>LP</namespace>

    <entity name="Book" local-service="true" remote-service="false">
        <!-- PK fields -->
        <column name="bookId" type="long" primary="true" />

        <column name="companyId" type="long" />
        <column name="groupId" type="long" />
        <column name="userId" type="long" />
        <column name="title" type="String" />
        <column name="createDate" type="Date" />
        <column name="modifiedDate" type="Date" />
    </entity>
</service-builder>
```
执行以下命令生成相关代码，需要为maven分配更大的运行内存，不然可能会执行失败。
``` bash
MAVEN_OPTS="-Xmx512m -XX:MaxPermSize=128m"
mvn liferay:build-service
```
此命令会生成`Book`相关的`model`、`service`以及数据库表创建脚本等内容。执行成功之后的目录结构如下：
``` bash
.
├── pom.xml
├── sample-portlet
│   ├── pom.xml
│   └── src
│       └── main
│           ├── java
│           │   └── com
│           │       └── zhaiyz
│           │           ├── model
│           │           │   └── impl
│           │           │       ├── BookBaseImpl.java
│           │           │       ├── BookCacheModel.java
│           │           │       ├── BookImpl.java
│           │           │       └── BookModelImpl.java
│           │           └── service
│           │               ├── base
│           │               │   ├── BookLocalServiceBaseImpl.java
│           │               │   └── BookLocalServiceClpInvoker.java
│           │               ├── impl
│           │               │   └── BookLocalServiceImpl.java
│           │               └── persistence
│           │                   └── BookPersistenceImpl.java
│           ├── resources
│           │   ├── META-INF
│           │   │   ├── base-spring.xml
│           │   │   ├── cluster-spring.xml
│           │   │   ├── hibernate-spring.xml
│           │   │   ├── infrastructure-spring.xml
│           │   │   ├── portlet-hbm.xml
│           │   │   ├── portlet-model-hints.xml
│           │   │   ├── portlet-orm.xml
│           │   │   ├── portlet-spring.xml
│           │   │   └── shard-data-source-spring.xml
│           │   ├── portlet.properties
│           │   └── service.properties
│           └── webapp
│               ├── css
│               │   └── main.css
│               ├── icon.png
│               ├── js
│               │   └── main.js
│               ├── view.jsp
│               └── WEB-INF
│                   ├── liferay-display.xml
│                   ├── liferay-plugin-package.properties
│                   ├── liferay-portlet.xml
│                   ├── portlet.xml
│                   ├── service.xml
│                   ├── sql
│                   │   ├── indexes.properties
│                   │   ├── indexes.sql
│                   │   ├── sequences.sql
│                   │   └── tables.sql
│                   └── web.xml
└── sample-portlet-service
    ├── pom.xml
    └── src
        └── main
            └── java
                └── com
                    └── zhaiyz
                        ├── model
                        │   ├── BookClp.java
                        │   ├── Book.java
                        │   ├── BookModel.java
                        │   ├── BookSoap.java
                        │   └── BookWrapper.java
                        ├── NoSuchBookException.java
                        └── service
                            ├── BookLocalServiceClp.java
                            ├── BookLocalService.java
                            ├── BookLocalServiceUtil.java
                            ├── BookLocalServiceWrapper.java
                            ├── ClpSerializer.java
                            ├── messaging
                            │   └── ClpMessageListener.java
                            └── persistence
                                ├── BookActionableDynamicQuery.java
                                ├── BookPersistence.java
                                └── BookUtil.java
```

### 打包发布并运行
执行以下命令，打包并发布至`LP_HOME`下的`deploy`目录。
``` bash
mvn package liferay:deploy
```
启动tomcat，在`deploy`下的war包会自动发布到webapps下。启动完成之后，数据库中就会存在一个名为`LP_Book`的表，其中`LP`为`service.xml`中定义的`namespace`，`Book`为`entry`的`name`属性值。查看此表定义如下：
```
mysql> desc LP_Book;
+--------------+-------------+------+-----+---------+-------+
| Field        | Type        | Null | Key | Default | Extra |
+--------------+-------------+------+-----+---------+-------+
| bookId       | bigint(20)  | NO   | PRI | NULL    |       |
| companyId    | bigint(20)  | YES  |     | NULL    |       |
| groupId      | bigint(20)  | YES  |     | NULL    |       |
| userId       | bigint(20)  | YES  |     | NULL    |       |
| title        | varchar(75) | YES  |     | NULL    |       |
| createDate   | datetime    | YES  |     | NULL    |       |
| modifiedDate | datetime    | YES  |     | NULL    |       |
+--------------+-------------+------+-----+---------+-------+
7 rows in set (0.00 sec)
```

---
全文完
