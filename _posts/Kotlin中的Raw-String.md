---
title: Kotlin中的Raw String
date: 2018-08-12 21:24:23
category:
- Kotlin
tags:
- Kotlin
---
在Kotlin中可以使用三个`"`开始，三个`"`结束来定义一个*Raw String*，如果要定义的字符串中包含需要进行转义的字符时，使用*Raw String*比*String*要方便一些。

比如需要定义一个字符串，来保存`{"gender":"男","name":"zhaiyz"}`，如果使用基本的字符串定义需要：
```
val stringJson = "{\"gender\":\"男\",\"name\":\"zhaiyz\"}"
```
字符串中的`"`需要使用`\"`进行转义，如果使用`Raw String`的方式进行定义需要：
```
val rawStringJson = """{"gender":"男","name":"zhaiyz"}"""
```
字符串中的`"`不需要再进行处理，以上两种方式的结果是等价的，但是明显使用`Raw String`的更加方便且可读性高。

<!-- More -->

编程中还会经常遇到定义一个包含换行的字符串，使用基本的字符串字符需要：
```
val stringNewline = "Hi,\nzhaiyz!"
```
使用`Raw String`的方式进行定义需要：
```
val rawStringNewline = """Hi,
zhaiyz!""
```
在Raw String中，换行符直接表现在字符串中的。此例过于简单，所以没能体现出`Raw String`的更好的可读性。
可以使用以下方法，定义出可读性更高的多行字符：
```
val rawStringNewlinePretty = """
    Hi,
    zhaiyz!
""".trimIndent()
```
其中`trimIndent()`方法可以把首行和尾行的空行以及每行前面的空白字符删除。最终得到的字符串与上面的等价。这样可读性就高了很多。

以下为代码示例：
``` Kotlin
fun main(args: Array<String>) {
    val stringJson = "{\"gender\":\"男\",\"name\":\"zhaiyz\"}"
    val rawStringJson = """{"gender":"男","name":"zhaiyz"}"""

    val stringNewline = "Hi,\nzhaiyz!"
    val rawStringNewline = """Hi,
zhaiyz!"""
    val rawStringNewlinePretty = """
        Hi,
        zhaiyz!
    """.trimIndent()

    println(stringJson == rawStringJson)
    println(stringNewline == rawStringNewline)
    println(stringNewline == rawStringNewlinePretty)
}
```
输出：
```
true
true
true
```
输出结果都为`true`，可见几种定义方式得到的结果是一样的。

以上只是以字符串中包含`"`和换行来举例说明`Raw String`的使用，像文章开始所说`Raw String`是可以用在使用基本`String`定义，需要进行一些转义操作时，让字符串的定义更方便，可读性更高。
