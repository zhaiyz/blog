---
title: Kotlin字符串模板
date: 2018-08-05 22:10:35
category:
- Kotlin
tags:
- Kotlin
---
在Kotlin中进行一些字符串拼接的时候，使用字符串模板会很简单。以`$`开始，直接根上变量名或是用`{}`包含表达示即可。代码示例：
``` Kotlin
fun main(args: Array<String>) {
    val name = "world"
    println("Hello $name!")
    println("Hello ${name.capitalize()}!")
}
```
输出：
```
Hello world!
Hello World!
```
如果想直接输出`$`，那么需要对`$`进行转义，使用`\$`。
代码：
``` Kotlin
println("Hello \$name!")
```
输出：
```
Hello $name!
```
字符串模板只是Kotlin的语法糖，`println("Hello $name!")`对应的字节码反编译为Java代码，相当于`String var2 = "Hello " + name + "!";`，只是方便了使用。

