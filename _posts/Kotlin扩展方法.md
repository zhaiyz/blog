---
title: Kotlin扩展方法
date: 2018-07-29 20:35:12
category:
- Kotlin
tags:
- Kotlin
---
Kotlin与Java相比有一个很高级的特性，就可以扩展方法。可以直接为一个类的所有对象添加方法。
比如以下代码可以为所有`String`类型对象添加一个`printIt()`方法，调用时打印其本身。
``` Kotlin
fun String.printIt() {
    println(this)
}
```
以上代码可以简写为
``` Kotlin
fun String.printIt() = println(this)
```
使用方式如下
``` Kotlin
fun main(args: Array<String>) {
    "Hello world!".printIt()
}
```
输出：`Hello world!`
在扩展方法里面`this`为调用者本身。

<!-- More -->

Kotlin的扩展方法在扩展一些第三方包和Java本身包里面的类方法时很有用。比如在JDK 1.8中新加入了`LocalDate`和`LocalDatetime`类型，方便了日期的处理，但使用时经常会遇到`Date`类型与这两种类型的转换。这时就可以定义几个扩展方法，方便使用。代码如下
``` Kotlin
fun LocalDate.toDate(zoneId: ZoneId = ZoneId.systemDefault()) = Date.from(atStartOfDay(zoneId).toInstant())

fun LocalDateTime.toDate(zoneId: ZoneId = ZoneId.systemDefault()) = Date.from(atZone(zoneId).toInstant())

fun Date.toLocalDate(zoneId: ZoneId = ZoneId.systemDefault()) = toInstant().atZone(zoneId).toLocalDate()

fun Date.toLocalDateTime(zoneId: ZoneId = ZoneId.systemDefault()) = toInstant().atZone(zoneId).toLocalDateTime()
```
以上方法中还使用到了Kotlin默认参数特性。
使用时很简单，代码如下：
``` Kotlin
fun main(args: Array<String>) {
    val date = Date()
    println(date.toLocalDate())
    println(date.toLocalDateTime())

    val localDate = LocalDate.now()
    println(localDate.toDate())

    val localDateTime = LocalDateTime.now()
    println(localDateTime.toDate())
}
```
输出：
```
2018-07-29
2018-07-29T20:50:19.957
Sun Jul 29 00:00:00 CST 2018
Sun Jul 29 20:50:20 CST 2018
```
