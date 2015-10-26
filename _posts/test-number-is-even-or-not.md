title: 测试一个整数是否为偶数
date: 2014-04-14 20:57:43
categories: java
tags: [java, even]
description: 测试一个整数是否为偶数
keywords: java, even
---
> 一般判断奇偶数是用`num % 2 == 0`来判断，如果为true则为偶数，为false则为奇数。还有一种通过位运算进行判断的方法，原理是偶数在二进制里面，最后一位为0，奇数则为1。所以可以通过与1做位与运算判断奇偶数。即`(num & 1) == 0`如果结果为true则为偶数，为false则为奇数。效率比取余运算高的多。 以下为测试代码。

``` java
public class Even {
	public static void main (String[] args) {
		System.out.println("1 is even: " + isEven(1));
		System.out.println("2 is even: " + isEven(2));
	}

	public static boolean isEven (int num) {
		return (num & 1) == 0;
	}
}

输出结果为：
1 is even: false
2 is even: true
```

--**EOF**--