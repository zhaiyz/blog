---
title: Kotlin包级函数
date: 2018-07-18 22:22:25
category:
- Kotlin
tags:
- Kotlin
---
Kotlin与Java最大的不同之一就是函数可以不需要定义在类中。本文就介绍下Kotlin的包级函数。

Kotlin中定义一个包级函数很简单：
``` Kotlin
package com.zhaiyz.demo

fun sayHello(name: String) {
    println("Hello $name!")
}
```
把以上内容保存在`Funs.kt`中。
在Kotlin中使用包级函数：
``` Kotlin
import com.zhaiyz.demo.sayHello

fun main(args: Array<String>) {
    sayHello("world")
}
```
可以`import`对应包下面的函数，直接使用。
在Java中使用Kotlin的包级函数：
``` Java
import com.zhaiyz.demo.FunsKt;

public class Demo {

    public static void main(String[] args) {
        FunsKt.sayHello("world");
    }
}
```
因为Java中函数必须通过类或对象调用，Kotlin的包级函数在Java中使用要通过Kotlin包级方法所在的文件名+Kt作为类引入，再进行调用，相当于使用静态函数。

Kotlin中的main函数，也是一个特殊的包级函数，可以做为程序的入口。
