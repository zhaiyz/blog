title: 数据库中保存多种状态或类型时使用int还是varchar
date: 2015-10-28 21:36:01
description: 数据库中保存多种状态或类型时使用int还是varchar
category:
- 设计
tags:
- 数据库
- mysql
---
在数据库设计过程中，基本上都会遇到一些叫作`状态`、`类型`之类的字段。比如说一篇文章会有`草稿`、`已发布`、`删除`等状态。如果使用`int`来保存这个字段的话，可以是`0`表示`草稿`，`1`表示`已发布`，`2`表示`已删除`。如果使用`varchar`来保存的话，可以是`DRAFT`表示`草稿`，`PUBLISHED`表示`已发布`，`DELETED`表示`已删除`。

使用`int`会比`varchar`占用的空间会小，而且使用`tinyint`或`smallint`也就够用了。使用`varchar`的话，在查看数据库的数据的时候，会更加直观。一般在设计数据库的时候，会在字段的`comment`中写出可以使用到的值以及各个值对应的含义。所以`int`值虽然一下看不懂，可以再看到`comment`中的说明即可。如果在此字段上建立索引，也是`int`效率会高一些。

<!--more-->

一般在开发的时候，会使用一个枚举来定义数据库保存的内容与实际含意的关系。这时使用`int`和`varchar`保存数据的区别会被封装起来。使用`int`时的枚举可能是这样的：
``` java
public enum ArticleStatus {

    /** 草稿 **/
    DRAFT(0, "草稿"),

    /** 已发布 **/
    PUBLISHED(1, "已发布"),

    /** 已删除 **/
    DELETED(2, "已删除");

    private int articleStatus;

    private String name;

    private ArticleStatus(int articleStatus, String name) {
        this.articleStatus = articleStatus;
        this.name = name;
    }

    // 其他方法
    .
    .
    .
}
```
使用`varchar`时的枚举可能是这样的：
``` java
public enum ArticleStatus {

    /** 草稿 **/
    DRAFT("DRAFT", "草稿"),

    /** 已发布 **/
    PUBLISHED("PUBLISHED", "已发布"),

    /** 已删除 **/
    DELETED("DELETED", "已删除");

    private String articleStatus;

    private String name;

    private ArticleStatus(String articleStatus, String name) {
        this.articleStatus = articleStatus;
        this.name = name;
    }

    // 其他方法
    .
    .
    .
}
```
使用这两种类型的区别就是枚举中第一个字段是什么类型。在程序中使用的时候，会用`ArticleStatus.DRAFT`来表示`草稿`状态。与数据库中数据对应的时候会使用`ArticleStatus.DRAFT.getArticleStatus()`，当需要显示给用户看的时候会使用`ArticleStatus.DRAFT.getName()`。

在网上也看到过关于使用这两种类型的优缺点。一般来说是如果需要在字段上建立索引，推荐使用`int`。如果说只是保存，再显示用，可以用`varchar`。我认为这类状态或类型字段，基本上都会用来做查询条件，所以说还是都使用`int`来保存吧。
