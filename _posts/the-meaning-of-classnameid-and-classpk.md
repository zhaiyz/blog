title: ClassNameId和ClassPK的意义
date: 2014-04-09 22:46:01
categories: liferay
tags: [liferay, classnameid, classpk]
description: ClassNameId和ClassPK的意义
keywords: liferay, classnameid, classpk
---
本文将介绍liferay中`classNameId`和`ClassPK`的意义。

Liferay中一些表中包含`classNameId`和`classPK`这两个字段，其中`classNameId`对应`ClassName_`表中的`classNameId`字段。`ClassName_`表中另一个字段是`value`，其值为一个model对象的全路径名，如`com.liferay.portal.model.Account`。每个model有一张表与之对应，如`Account_`。`classPK`的意思就是这张表的主键。

如上所述，通过`classNameId`和`classPK`这两个字段就能定位一条entity记录。

### 参考文献
1. [What is classPK?](https://www.liferay.com/zh/community/forums/-/message_boards/message/679177)

---
全文完
