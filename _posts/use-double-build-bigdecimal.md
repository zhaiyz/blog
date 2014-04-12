title: 使用double构建一个BigDecimal
date: 2014-04-07 21:22:25
categories: java
tags: [java, bigdecimal]
description: 使用double构建一个BigDecimal
keywords: java, bigdecimal
---
使用`new BigDecimal(double val)`得到`BigDecimal`并不是想像结果一样。以下为测试代码：
``` java
import java.math.BigDecimal;

public class BigDecimalTest {
	public static void main(String[] args) {
		System.out.println("new BigDecimal(\"1.1\") = " + new BigDecimal("1.1"));
		System.out.println("new BigDecimal(1.1) = " + new BigDecimal(1.1));
		System.out.println("BigDecimal.valueOf(1.1) = " + BigDecimal.valueOf(1.1));
	}
}
```
编译执行，结果为：
```
new BigDecimal("1.1") = 1.1
new BigDecimal(1.1) = 1.100000000000000088817841970012523233890533447265625
BigDecimal.valueOf(1.1) = 1.1
```
可以看到`new BigDecimal(1.1)`的结果不是想要得到的`1.1`。如果想得到一个精确的`BigDecimal`那么使用`new BigDecimal(String val)`，即使用一个字符串类型作为参数，如果必须使用`double`作参数，那么使用`BigDecimal valueOf(double val)`，如`BigDecimal.valueOf(1.1)`。

---
全文完