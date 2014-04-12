title: "nutz中ioc的Json配置文件格式"
id: 121
date: 2012-03-04 01:21:34
tags: 
- ioc
- json
- nutz
categories: 
- nutz
---

首发于**iteye**，链接：[http://zhaiyz.iteye.com/blog/1428117](http://zhaiyz.iteye.com/blog/1428117 "nutz中ioc的Json配置文件格式")
最近学习了下[nutz](http://code.google.com/p/nutz/) ，感觉很不错，入门第一步肯定是Hello world。我在学ioc的[Hello world](http://code.google.com/p/nutz/wiki/ioc_hello) 的时报了个警告：
``` java
log4j: 2012-02-27 23:19:38,366 [main] WARN org.nutz.ioc.IocLoading - Using *Declared* ioc-define (without type or events)!!! Pls use Standard Ioc-Define!! Bean will define as:
{
    "singleton" :true,
    "args" :[],
    "fields" :[{
        "name" :"name",
        "value" :{
        "type" :"normal",
        "value" :"XiaoBai"
    }
    }, {
        "name" :"birthday",
        "value" :{
            "type" :"normal",
            "value" :"2009-10-25 15:23:40"
        }
    }]
}
```

警告的意思是“使用了声明式的ioc定义，请使用标准的ioc定义”，那么什么是标准的ioc定义呢，[Hello world](http://code.google.com/p/nutz/wiki/ioc_hello) 的下一节[匿名对象](http://code.google.com/p/nutz/wiki/ioc_inner_object)就说了：如果配置文件解析成map后的键值仅包含“type、scope、singleton、fields、args、events”中的一个或几个字段，就是个标准的ioc定义。
<!--more-->
报之上的警告是因为在ioc的配置文件中，使用了：
``` json
xiaobai : {
    name : 'XiaoBai',
    birthday : '2009-10-25 15:23:40'
}
```

这样，name和birthday就会被当作map的键值，它们不包含在“type、scope、singleton、fields、args、events”之内。

可以修改为：
``` json
xiaobai : {
    fields : {
        name : 'XiaoBai',
        birthday : '2009-10-25 15:23:40'
    }
}
```

这样的话，fields就是会成为解析后map的键值，就不会报开始的那个警告。

我跟了下代码，在nutz-1.b.42.jar（我使用的是这个版本）org.nutz.ioc包里面的Iocs虚拟类中（应该作为工具类，防止 实例化才定义为虚拟类的，不过这种可以直接把其默认构造器私有化来实现，不用搞个虚拟类）有个方法就是用来检测是否为标准的ioc定义。
``` java
/**
* @author zozoh(zozohtnt@gmail.com)
* @author wendal(wendal1985@gmail.com)
*
*/
public abstract class Iocs {

private static final String OBJFIELDS = "^(type|scope|singleton|fields|args|events)$";

    public static boolean isIocObject(Mapmap) {
        for (Entry en : map.entrySet())
            if (!en.getKey().matches(OBJFIELDS))
                return false;
        return true;
    }
    // 此处省略其他方法
}
```

意思很明白，和以上所说的一样，如果map的key不包含在"type|scope|singleton|fields|args|events"中就返回false。在同一个包下的IocLoading类的map2iobj方法有如下判断：
``` java
@SuppressWarnings("unchecked")
public IocObject map2iobj(Map map) throws ObjectLoadException {
    final IocObject iobj = new IocObject();
    if (!isIocObject(map)) {
        for (Entry en : map.entrySet()) {
            IocField ifld = new IocField();
            ifld.setName(en.getKey());
            ifld.setValue(object2value(en.getValue()));
            iobj.addField(ifld);
        }
        if(log.isWarnEnabled()) //TODO 移除这种兼容性
            log.warn("Using *Declared* ioc-define (without type or events)!!! Pls use Standard Ioc-Define!!" +
" Bean will define as:\n"+Json.toJson(iobj));
    }// 此处省略其他代码
}
```

开始的WARN就是这打出来的。

这个应该是历史遗留问题，作者也不推荐使用了，所以还是按标准的来。不过也相当简单，就那几个字段，照着配好就行。