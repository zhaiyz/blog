---
title: Kotlin默认参数方法
date: 2018-07-21 16:03:42
category:
- Kotlin
tags:
- Kotlin
---
Kotlin中参数是可以设置默认值的，设置默认值的参数，如果没有传就使用默认值。
示例代码，保存在Funs.kt中：
``` Kotlin
fun sayHello(name: String = "world") {
    println("Hello $name!")
}
```
调用以上代码时，可以有两种方式，如下：
``` Kotlin
fun main(args: Array<String>) {
    sayHello()
    sayHello("zhaiyz")
}
```
输出：
```
Hello world!
Hello zhaiyz!
```
`sayHello()`没有传参，`name`就使用`world`做为值，如果传入了参数，就使用参数值。

但是以上方法在Java中调用的时候，只有`sayHello(String name)`方法，如果想在Java中使用不传默认参数的方法，需要在方法上加上`@JvmOverloads`，这样Kotlin编译的时候，会生成一个不需要当前默认值的重载方法，之后就可以在Java中使用没有默认参数的方法了。

<!-- More -->

如果有多个默认参数，而且只用到后面的参数时，需要指定参数名设值。
示例代码：
``` Kotlin
fun sayHello(name: String = "world", repeat: Int = 1) {
    repeat(repeat) {
        println("Hello $name!")
    }
}
```
调用时，如果只想传`repeat`参数，需要使用以下代码：
```
fun main(args: Array<String>) {
    sayHello(repeat = 2)
}
```
输出：
```
Hello world!
Hello world!
```



