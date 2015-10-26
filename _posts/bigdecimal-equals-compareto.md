title: BigDecimal类型数据大小比较
date: 2014-04-17 20:35:05
categories: java
tags: [java, bigdecimal]
description: BigDecimal类型数据大小比较
keywords: java, bigdecimal
---
> 在进行精确数值计算时，需要使用`BigDecimal`类型。本文将介绍`BigDecimal`类型的比较。

### 使用equals和compareTo比较两个`BigDecimal`类型数据
``` java
import java.math.BigDecimal;

public class BigDecimalDemo {
	public static void main(String[] args) {
		BigDecimal bd1 = new BigDecimal("2.10");
		BigDecimal bd2 = new BigDecimal("2.1");

		System.out.println("bd1 equals bd2: " + bd1.equals(bd2));
		System.out.println("bd1 compareTo bd2: " + bd1.compareTo(bd2));
	}
}

输出结果：
bd1 equals bd2: false
bd1 compareTo bd2: 0
```
由结果可以看出`equals`方法会比较两个数据的`scale`(精度)，而`compareTo`是对两个数据的数值进行比较，不比较它们的`scale`。

### 总结
在电子商务中进行价格计算的时候经常会使用到此种数据，进行两个价格进行比较时，需要使用`compareTo`。

--**EOF**--
