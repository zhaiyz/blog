---
title: Kotlin中List转Map的常用方式
date: 2018-07-30 21:42:13
category:
- Kotlin
tags:
- Kotlin
---
在开发中，经常用到把一个`List`按一定规则转换为`Map`来使用。本文就介绍下几种常用的转换方式。
代码如下：
``` Kotlin
data class User(val id: Long, val name: String, val age: Int)

fun main(args: Array<String>) {

    val users = listOf(User(1, "张三", 20), User(2, "李四", 20), User(3, "王五", 25), User(4, "赵六", 25))

    // 变为以id为key, user为value的map，类型为Map<Long, User>
    println(users.associateBy { it.id })

    // 变为以id为key，name为value的map，类型为Map<Long, String>
    println(users.associate { it.id to it.name })

    // 可以自定义key和value的map，类型为Map<String, String>
    println(users.associateBy({ "id:${it.id}" }, { "name:${it.name}" }))

    // 生成按age聚合，对象List为value的map，类型为Map<Int, List<User>>
    println(users.groupBy { it.age })
}
```
输出：
```
{1=User(id=1, name=张三, age=20), 2=User(id=2, name=李四, age=20), 3=User(id=3, name=王五, age=25), 4=User(id=4, name=赵六, age=25)}
{1=张三, 2=李四, 3=王五, 4=赵六}
{id:1=name:张三, id:2=name:李四, id:3=name:王五, id:4=name:赵六}
{20=[User(id=1, name=张三, age=20), User(id=2, name=李四, age=20)], 25=[User(id=3, name=王五, age=25), User(id=4, name=赵六, age=25)]}
```
转成的Map其实都是`LinkedHashMap`，看输出的结果也可以看出来，生成的Map中的对象顺序和List中的一致。
当key的重复的时候，后面的值覆盖前面的值。比如添加一行代码:
```
println(users.associateBy { it.age })
```
来使用`age`字段当作key，其中id为1和2的age重复，id为3和4的age重复，生成map的时候，会保留下id为2和4的，id为1和3的值被覆盖了。此行代码的输出为
```
{20=User(id=2, name=李四, age=20), 25=User(id=4, name=赵六, age=25)}
```