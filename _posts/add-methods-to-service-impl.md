title: Liferay添加自定义服务层方法
date: 2014-04-02 21:34:28
categories: liferay
tags: [liferay, method, service]
description: Liferay添加自定义服务层方法
keywords: liferay, method, service
---
本文将介绍在service层添加自定义方法。

### 开发环境
* OS：ubuntu 12.04 64位
* Liferay Portal：6.2.0-ce-ga1

### 创建portlet
按照[Liferay Service Builder](http://zhaiyz.com/2014/04/01/liferay-service-builder/)一文中的步骤创建拥有一个`Book`实体的`servicebuilder-portlet`。

### 添加服务层方法
在`BookLocalServiceImpl.java`中添加一个`addBook`方法，以下为方法代码：
``` java
package com.zhaiyz.service.impl;

import java.util.Date;

import com.zhaiyz.model.Book;
import com.zhaiyz.service.base.BookLocalServiceBaseImpl;
import com.liferay.counter.service.CounterLocalServiceUtil;
import com.liferay.portal.kernel.exception.PortalException;
import com.liferay.portal.kernel.exception.SystemException;
.
.
.
public class BookLocalServiceImpl extends BookLocalServiceBaseImpl {
    public Book addBook(long companyId, long groupId, long userId, String title) throws PortalException, SystemException {
        long bookId = CounterLocalServiceUtil.increment(Book.class.getName());
        Date now = new Date();
        Book book = bookPersistence.create(bookId);

        book.setCompanyId(companyId);
        book.setGroupId(groupId);
        book.setUserId(userId);
        book.setTitle(title);
        book.setCreateDate(now);
        book.setModifiedDate(now);

        return bookPersistence.add(book);
    }
}
```
<!-- more -->
在`BookServiceImpl`中添加完方法还不能直接使用。需要运行以下命令生成相关的代码再使用`BookLocalServiceUtil`类使用添加的方法。为了防止出现`Exception in thread "main" java.lang.OutOfMemoryError: PermGen space`异常，需要设置`MAVEN_OPTS`参数。
``` bash
MAVEN_OPTS="-Xmx512m -XX:MaxPermSize=256m"
mvn liferay:build-service
```
`liferay:build-service`只是生成代码，并不会编译，如果要验证生成的代码是否能编译通过，需要执行`mvn package`命令。所有命令执行成功之后，就可以在业务层使用新添加的方法：
``` java
BookLocalServiceUtil.addBook(companyId, groupId, userId, title);
```

### 参考文章
* [Liferay Portal 6.0 - Development Guide - Service Builder](http://www.liferay.com/zh/documentation/liferay-portal/6.0/development/-/ai/service-build-2)

---
全文完