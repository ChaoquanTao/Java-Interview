---
title: 知识点汇总
date: 2019-09-04 09:27:46
updated: 2019-09-04 09:27:46
tags: 面经
categories: Java

---

### 自动拆装箱

- 为什么Java中有自动拆装箱

Java是一门面向对象的语言，如果只有八种基本类型`byte`,  `short`,`int`, `long`, `float`, `double`, `char`, `bool`，在计算上是简单的，但是在面向对象的操作上是麻烦的，比如向集合类添加元素就只能添加包装类型而不能添加基本类型。反之，包装类型是对象，存放在堆上，占用空间大，而基本类型存放在栈中。

- 包装类型和基本类型之间的比较

包装类型和包装类型比较，比较的是对象的地址；包装类型和基本类型比较，是先将包装类型拆箱再同基本类型比较。



### `String`, `StringBuffer` 和 `StringBuilder`

#### 1. 比较

`String`定义的字符串，不可修改；`StringBuffer`和`StringBuilder`定义的字符串，可以修改，但是`StringBuffer`是线程安全的。

解释：

上述三者底层都是通过定义了一个字节数组`byte[] value`来实现的，不同的是,对于`String`类型，数组被`final`修饰，不可修改，而`StringBuffer`和`StringBuilder`没有这个修饰。

`StringBuffer`和`StringBuilder`内容都可以修改，但是`StringBuffer`是线程安全的，因为它的`append()`方法被[`synchronized`](#synchronized)关键字修饰。

#### 2. 关于`String`

- `String s = new String("taochq");`定义了几个对象？

检查字符串常量池是否有`“taochq”`这个变量，有则返回其引用，此时定义了一个对象，没有则先创建后返回，定义了两个对象。

- 如何理解`String`的`intern`方法

检查当前字符串常量是否在常量池中，不在的话放入常量池并返回引用，在的话直接返回引用。它更多的是用于将那些只有在运行时才能确定的字符串放入常量池。

- `String s = "a"+"b"`定义了几个对象

一个，编译器进行了优化，就是`"ab"`。

- String s= new String("tao")+"chq"定义了几个对象

如果常量池中没有`"tao"`和`"chq"`的话，三个。

jdk7以后，字符串常量池放在了堆中



### `synchronized`

