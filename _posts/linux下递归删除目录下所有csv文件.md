title: "linux下递归删除目录下所有csv文件"
id: 131
date: 2012-03-04 22:59:31
tags: 
- linux
categories: 
- linux
---

原文地址：[http://www.cnblogs.com/yuepeng/archive/2011/04/08/2009034.html](http://www.cnblogs.com/yuepeng/archive/2011/04/08/2009034.html "linux下递归删除目录下所有exe文件")

因为项目有一些每日都要发送的报文，时间长了硬盘就不够用了，所以要删除些。文件很多，主要还是因为在不同的目录里面，不方便一下全部删除。现找到这么一条语句来完成此功能，如下
``` bash
find . -name '*.csv' -type f -print -exec rm {} \;
```

1.  "."    表示从当前目录开始递归查找
2.  "-name '*.csv' "根据名称来查找，要查找所有以.csv结尾的文件夹或者文件
3.  " -type f "查找的类型为文件
4.  "-print" 输出查找的文件目录名
5.  最主要的是是-exec了，-exec选项后边跟着一个所要执行的命令，表示将find出来的文件或目录执行该命令。exec选项后面跟随着所要执行的命令或脚本，然后是一对儿{}，一个空格和一个\，最后是一个分号