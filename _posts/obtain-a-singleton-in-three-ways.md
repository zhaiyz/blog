title: 取得一个单例的三种方式
date: 2014-04-15 21:28:27
categories: java
tags: [java, singleton]
description: 取得一个单例的三种方式
keywords: java, singleton
---
> 开发中经常需要获取一个单例的对象。本文将介绍得到单例对象的方法。

### Early Initialization
``` java
public class SingletonEarly {

	private final static SingletonEarly instance = new SingletonEarly();

	private SingletonEarly() {
	}

	public static SingletonEarly getInstance() {
		return instance;
	}
    
}
```
使用方式：
``` java
SingletonEarly.getInstance();
```
<!-- more -->
### Lazy Initialization
``` java
public class SingletonLazy {

	private volatile static SingletonLazy instance;

	private SingletonLazy() {
		// Suppressing creating a new instances
	}

	public static SingletonLazy getInstance() {
		if (instance == null) {
			synchronized (SingletonLazy.class) {
				if (instance == null) {
					instance = new SingletonLazy();
				}
			}
		}
		return instance;
	}

}
```
使用方式：
``` java
SingletonLazy.getInstance();
```

### Enum Singleton
``` java
public enum SingletonEnum {
	
	INSTANCE;

}
```
使用方式：
``` java
SingletonEnum.INSTANCE;
```

### 总结
单例模式中，使用枚举是最好的方式，原因可以参考[单例模式中为什么用枚举更好](http://www.importnew.com/6461.html)。不过需要JDK1.5或以上版本支持。

### 参考文献
1. [Singleton](http://coderevisited.com/singleton/)

--**EOF**--
