---
title: 使用DecimalFormat格式化小数
date: 2018-07-16 21:26:59
category:
- 开发
tags: 
- DecimalFormat
---
开发中会遇到一些需要对小数进行格式化的地方，这时可以使用`DecimalFormat`。此文记录一个使用`DecimalFormat`格式化小数时的一个注意事项。

比如现在有两个小数`1.25`和`1.15`，需要四舍五入保留一位小数。可以使用以下kotlin代码：
``` kotlin
fun main(args: Array<String>) {
    val number1 = 1.25
    val number2 = 1.15
    val decimalFormat = DecimalFormat("0.0")
    println(decimalFormat.format(number1))
    println(decimalFormat.format(number2))
}
```
但是以上代码的输入为:
```
1.2
1.2
```
和预期的不一样。这是因为`DecimalFormat`默认的`RoundingMode`为`RoundingMode.HALF_EVEN`。API中的解释为:
```
Rounding mode to round towards the "nearest neighbor" unless both neighbors are equidistant, in which case, round towards the even neighbor. Behaves as for RoundingMode.HALF_UP if the digit to the left of the discarded fraction is odd; behaves as for RoundingMode.HALF_DOWN if it's even. 
```
如果要四舍五入，需要显示的设置`RoundingMode`为`RoundingMode.HALF_UP`，最终代码为：
``` kotlin
fun main(args: Array<String>) {
    val number1 = 1.25
    val number2 = 1.15
    val decimalFormat = DecimalFormat("0.0")
    decimalFormat.roundingMode = RoundingMode.HALF_UP
    println(decimalFormat.format(number1))
    println(decimalFormat.format(number2))
}
```
以上代码的输入为：
```
1.3
1.2
```
符合预期。
