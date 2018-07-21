---
title: Kotlin中定义静态方法
date: 2018-07-17 21:45:54
category:
- Kotlin
tags:
- Kotlin
---
开发过程中经常要写一些工具类，里面定义一些静态方法。本文介绍下在Kotlin中定义静态方法的方式。
可以使用以下两种方式：
1. 使用`object`，比如：
``` kotlin
object Utils {
    fun sayHello(name: String) {
        println("Hello $name!")
    }
}
```
2. 使用`companion object`
``` kotlin
class Utils {
    companion object {
        fun sayHello(name: String) {
            println("Hello $name!")
        }
    }
}
```
在Kotlin中使用调用方式是一样的：
``` kotlin
fun main(args: Array<String>) {
    Utils.sayHello("world")
}
```
在Java中调用时，如果使用`object`：
``` java
    public static void main(String[] args) {
        Utils.INSTANCE.sayHello("world");
    }
```
如果使用`companion object`：
``` java
    public static void main(String[] args) {
        Utils.Companion.sayHello("world");
    }
```
