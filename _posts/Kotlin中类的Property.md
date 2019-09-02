---
title: Kotlin中类的Property
date: 2018-08-07 21:47:24
category:
- Kotlin
tags:
- Kotlin
---
开发中经常需要定义一些POJO，里面只有基本字段及对应的setter/getter方法。比如以下代码是使用Java定义一个包含姓名、生日两个字段的类：
``` Java
public class User {

    private String name;

    private Date birthday;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Date getBirthday() {
        return birthday;
    }

    public void setBirthday(Date birthday) {
        this.birthday = birthday;
    }
}
```
如果使用Kotlin定义相同功能的类只需要以下代码：
``` Kotlin
class User {

    var name: String? = null

    var birthday: Date? = null
}
```
可以看出Kotlin定义简洁了很多。
在Java中`name`、`birthday`叫作`field`，而在Kotlin中叫作`property`。使用`var`定义的`property`直接可以通过变量名进行赋值和取值。以下代码可以初始化一个User对象：
``` Kotlin
fun main(args: Array<String>) {
    val user = User()
    user.name = "zhaiyz"

    println("User: name = ${user.name}")
}
```
输出：
```
User: name = zhaiyz
```
可以看出来，使用起来很方便。

<!-- More -->

当一个property在赋值或取值需要进行一些处理的时候，可以重写它的set或get方法。比如想在设置`name`的时候，进行一些处理，可以重写`name`property的set方法，使用以下代码：
``` Kotlin
    var name: String? = null
        set(value) {
            field = "My name is $value"
        }
```
注意上面代码段中的**`field`**字段，它代表了property的值，而不是property名`name`。再次运行之前的`main`方法，输出为：
```
User: name = My name is zhaiyz
```
可以看出，name的值添加上了`My name is `。
同样也可以重写property的get方法来改变最后得到的结果，比如以下代码可以在取生日property值时，如果没有值就返回当前时间。
``` Kotlin
    var birthday: Date? = null
        get() {
            return field ?: Date()
        }
```
同样，**`field`**字段为当前property的值。实例化一个User对象，不进行任何赋值操作，打印`birthday`时也会有值。运行以下代码：
```
fun main(args: Array<String>) {
    val user = User()

    println("User: birthday = ${user.birthday}")
}
```
输出为：
```
User: birthday = Tue Aug 07 22:27:00 CST 2018
```

Kotlin中的property功能上与Java的field加上setter/getter方法一样，但是使用变得简洁了很多。
