title: "s:property标签显示html代码"
id: 151
date: 2012-06-26 20:27:03
tags: 
- struts
categories: 
- code
---

如果一个属性的值是一段html代码，想在页面上被解析出来，只需要把s:property标签的escape属性设置为false。
``` java
<s:property value="html" escape="false"/>
```