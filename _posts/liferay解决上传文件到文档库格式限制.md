title: "liferay解决上传文件到文档库格式限制"
id: 152
date: 2012-06-27 20:10:54
tags: 
categories: 
- liferay
---

默认情况下文档库不支持flv文件格式，只需要在portal-ext.properties文件中添加下配置
``` bash
dl.file.extensions=.ftl,.bmp,.css,.doc,.docx,.dot,.gif,.gz,.htm,.html,.jpg,.js,.lar,.mp3,.odb,.odf,.odg,.odp,.ods,.odt,.pdf,.png,.ppt,.pptx,.pps,.ppsx,.ppsm,.rtf,.swf,.sxc,.sxi,.sxw,.tar,.tiff,.tgz,.txt,.vsd,.xls,.xlsx,.xml,.zip,.jrxml,.flv
```
其他的一些文件格式也能这样配置。