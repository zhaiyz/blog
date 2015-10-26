title: 把博客从wordpress中迁移到hexo中
date: 2014-04-12 22:41:40
categories: hexo
tags: [hexo, wordpress]
description: 把博客从wordpress中迁移到hexo中
keywords: hexo, wordpress
---
> 由于之前用wordpress写过博客，现在在用hexo。想把之前的博客迁移到hexo中，而且hexo也有这样的插件。本文将介绍迁移方法。

### 安装WordPress migrator插件
执行以下命令，安装WordPress migrator插件
``` bash
npm install hexo-migrator-wordpress --save
```

### 从wordpress中导出文章
登录wordpress管理控制台，选择工具->导出，再选择文章[如下图]。点击下载导出的文件，就可以得到一个名称类似`wordpress.2014-04-12.xml`的文件。

![wordpress_export](http://zhaiyz.qiniudn.com/images/blog/20140412/wordpress_export.png)

<!-- more -->

### 把文章导入到hexo
在hexo生成的站点目录，即hexo init <站点目录>中的站点目录。执行以下命令，source为上一步中导出的类似`wordpress.2014-04-12.xml`文件全路径。
``` bash
hexo migrate wordpress source
```
执行完成之后，在站点目录->source->_posts目录中，就可以看到导入的文章。

### 后话
此插件功能很是强大，不光文章标题，内容能够迁移过来，文章的写作日期，包含的标签，所属的分类也可以自动导入。文章内容的格式也可以转换为markdown格式。需要修改的地方只是包含代码的部分。wordpress中使用的是Syntax Highlighter，代码段是用类似[java][/java]的标签包围起来的，换成用前后各三个` ` `包含起来即可。本站的14年之前的文章都是利用此方法导入进来的。

### 参考文献
1. https://github.com/hexojs/hexo-migrator-wordpress
