title: Liferay定制数据库字段长度
date: 2014-04-03 21:47:45
categories: liferay
tags: [liferay, database, column, size]
description: Liferay定制数据库字段长度
keywords: liferay, database, column, size
---
本文将介绍改变数据库字段默认长度。

### 开发环境
* OS：ubuntu 12.04 64位
* Liferay Portal：6.2.0-ce-ga1
* Mysql：5.5.35

### 创建portlet
按照[Liferay Service Builder](http://zhaiyz.com/2014/04/01/liferay-service-builder/)中的步骤创建拥有一个`Book`实体的portlet。

### 自定义字段长度
在`service.xml`文件如果有字段的类型为`String`，如
``` xml
<column name="title" type="String" />
```
那么生成数据库表时，`title`字段的长度默认为`75`。如果要改变默认长度，需要修改`sample/sample-portlet/src/main/resources/META-INF`目录下的`portlet-model-hints.xml`文件内容。现修改为如下内容：
``` xml
<?xml version="1.0"?>

<model-hints>
	<model name="com.zhaiyz.model.Book">
		<field name="bookId" type="long" />
		<field name="companyId" type="long" />
		<field name="groupId" type="long" />
		<field name="userId" type="long" />
		<field name="title" type="String">
			<hint name="max-length">255</hint>
		</field>
		<field name="createDate" type="Date" />
		<field name="modifiedDate" type="Date" />
	</model>
</model-hints>
```
<!-- more -->
修改完成之后，需要再次执行以下命令，重新生成代码及数据库脚本打包并部署。
``` bash
mvn liferay:build-service package liferay:deploy
```
成功执行完以上命令后，再启动tomcat，启动成功后，再查看数据库的`LP_Book`表，结果如下：
```
mysql> desc LP_Book;
+--------------+--------------+------+-----+---------+-------+
| Field        | Type         | Null | Key | Default | Extra |
+--------------+--------------+------+-----+---------+-------+
| bookId       | bigint(20)   | NO   | PRI | NULL    |       |
| companyId    | bigint(20)   | YES  |     | NULL    |       |
| groupId      | bigint(20)   | YES  |     | NULL    |       |
| userId       | bigint(20)   | YES  |     | NULL    |       |
| title        | varchar(255) | YES  |     | NULL    |       |
| createDate   | datetime     | YES  |     | NULL    |       |
| modifiedDate | datetime     | YES  |     | NULL    |       |
+--------------+--------------+------+-----+---------+-------+
7 rows in set (0.00 sec)
```
可以看到`title`字段的长度已经变为`255`。还有别一种配置方法可以完成同样的功能，配置如下：
```
<?xml version="1.0"?>

<model-hints>
	<hint-collection name="VARCHAR-255">
        <hint name="max-length">255</hint>
    </hint-collection>

	<model name="com.zhaiyz.model.Book">
		<field name="bookId" type="long" />
		<field name="companyId" type="long" />
		<field name="groupId" type="long" />
		<field name="userId" type="long" />
		<field name="title" type="String">
			<hint-collection name="VARCHAR-255" />
		</field>
		<field name="createDate" type="Date" />
		<field name="modifiedDate" type="Date" />
	</model>
</model-hints>
```
实际开发中，推荐使用这种方法。

### 更多
在`portlet-model-hints.xml`文件中还能对字段进行更多的配置，如`default-value`、`display-height`、`display-width`等属性。更多内容，请阅读[Customize DB Column Sizes ](http://www.liferay.com/zh/community/wiki/-/wiki/Main/Customize+DB+Column+Sizes)。

### 参考文章
[Customize DB Column Sizes ](http://www.liferay.com/zh/community/wiki/-/wiki/Main/Customize+DB+Column+Sizes)。

---
全文完