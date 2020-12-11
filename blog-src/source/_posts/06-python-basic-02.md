---
layout: post
title: Re:从零开始的Python3学习笔记 02
date: 2020-03-16 15:40:00
updated: 2020-03-16 16:45:00
description: <blockquote><h3><center>Python3 基础学习笔记（二） -- 快速上手：Python基础知识2</center></h3></blockquote><br />本节记录了本节记录了函数和模块、经典的海龟绘图、简单的数据类型转换。
categories: 
- [Python学习笔记, 基础学习]
tags: 
- python
- 语言基础
cover: true
thumbnail: "https://cdn.idealx.cn/blogimage/python/python-icon.png"
permalink: python/basic-02.html
---
<blockquote><center>Python3 基础学习笔记（二） -- 函数、模块</center></blockquote>

## - 1.5 函数

在 Python 中，像 C 语言一样，我们称为函数；在 Java 中，我们称为方法。

这里记录几个比较简单的函数，后面会遇到各种各样的函数和函数库。

##### pow 函数

函数 pow 相当于 **乘方** （power）运算。它可以 用于编写数值表达式。

```python
>>> 2 ** 10
1024
>>> pow(2, 10)
1024
```

像 pow 函数这样的标准函数，称为 **内置函数** 。

##### abs 函数

函数 abs 计算 **绝对值** （absolute value） ，绝大多数编程语言甚至 excel 中的公式都是这样。

```python
>>> abs(-1024)
1024
```

##### round 函数

函数 round 将浮点数圆整为与之 **最接近** 的整数。

```python
>>> 5 // 3
1
>>> round(5/3)
2
```

整除总是向下圆整，round函数总是向最近的整数圆整。

##### int 函数

函数 int 将浮点数转换向下圆整为整数。

```python
>>> int(19.9)
19
```

其他向下圆整和向上圆整的函数将在「模块」部分记录。


## - 1.6 模块

使用 `import` 命令使用模块。模块 是 基础函数 的扩展，通过将其导入可以扩展 Python 的功能。（就像 Java 的import 一样）

### - 1.6.1 import 命令

```python
>>> import math
>>> math.floor(20.9) # 向下圆整
20
>>> math.ceil(20.4) # 向上圆整
21
```

如果确定不会从不同的模块导入多个同名函数，可能不想每次调用函数时都指定函数名。这种情况下，需要使用`import` 命令的变种 `from module import function` 。

##### sqrt 函数

函数 sqrt 计算 平方根（square root） 

```python
>>> from math import sqrt
>>> sqrt(16)
4.0
```

### - 1.6.2 使用变量引用函数

在 Python 中可以使用变量来引用函数（以及其他大部分的 Python 元素）。

```python
>>> XD = math.sqrt # 变量XD
>>> XD(4)
2.0
```

### - 1.6.3 复数 和 cmath

函数 sqrt 用于计算平方根，但它仅限于 **实数** 领域。

```python
>>> sqrt(-2)
Traceback (most recent call last):
  File "<pyshell#15>", line 1, in <module>
    sqrt(-2)
ValueError: math domain error # 这是报错信息
```

直接使用 math 函数库中的 sqrt 函数会报错，有些平台可能显示 `nan` （非数值 not a number）。

如果是复数（complex number）的话，Python 标准库提供了一个专门用于处理复数的模块。

```python
>>> import cmath
>>> cmath.sqrt(-1)
1j
>>> (1 + 3j) * (10 + 2j)
(4+32j)
```

1j 是一个虚数，虚数以 j 或者 J 结尾。

> Python 本身提供了对复数的支持，Python 没有专门表示虚数的类型，而将虚数视为实部为零的复数。

**以上演示都在交互式解释器中执行。当然，也可以创建一个 `.py` 文件，像创建 C 程序或 Java 程序一样。**

### - 1.6.4 海龟绘图法

Python 有一些有趣的玩意儿，比如海龟（turtle）。它的绘画功能十分不可思议。

```python
# turtle_01.py 画出一个三角形
import turtle
t=turtle.Pen()
t.forward(100)
t.left(120)
t.forward(100)
t.left(120)
t.forward(100)
```

会看到一个三角形的物体在移动，那就是海龟，哈哈哈哈。

再画一些有趣的东西。

```python
# NiceHexSpiral.py
import turtle
colors=['red','purple','blue','green','yellow','orange']
t=turtle.Pen()
turtle.bgcolor('black')
for x in range(360):
    t.pencolor(colors[x%6])
    t.width(x/100+1)
    t.forward(x)
    t.left(59)
```

这是一个彩色螺旋线的 Demo，可以看到 Python 语言来实现它真的非常容易。

> 其中涉及的列表、循环语句等将在后面记录。

## - 1.7 数据类型转换

当一种类型的数据被使用时，有时需要将其转换为其他类型的数据。Python 提供了一些内置函数。

1、转化为整数：函数 `int(x)`，x 为数字或字符串型的数字，但不支持复数。

```python
>>> int(5.2)
5	# 小数部分丢弃
>>> int('20')
20
```

2、转化为浮点数：函数 `float(x)`，x 为数字或字符串型的数字，但不支持复数。

```python
>>> float(50)
50.0
>>> float('20.5')
20.5
```

3、转化为复数：函数 `complex(x,y)`，x、y为整数、浮点数、布尔数；当只有 x 参数时 (y=0) 可以是**字符串型整数**、浮点数、布尔数。

```python
>>> complex(2,5)
(2+5j)
>>> complex('20')
(20+0j)
```

4、转化为字符串：函数`str(x)`，在将数字拼接进字符串时一定要用。

```python
>>> str(2+5j)
'(2+5j)'
```

> 在python2版本中不支持二进制、八进制和十六进制数字的转化。

5、转化为二进制数：函数 `bin(x)`，x 为非负整数。

```python
>>> bin(3)
'0b11'
```

6、转化为八进制数：函数 `oct(x)`，x 为非负整数。

```python
>>> oct(10)
'0o12'
```

7、转化为十六进制：函数 `hex(x)`，x 为非负整数。

```python
>>> hex(20)
'0x14'
```

8、将十进制数转化为 ASCII 码：函数 `chr(x)`，x 为十进制数。

```python
>>> chr(98)
'b'
```

9、将 ASCII 码转化为十进制数：函数 `ord(x)`，x 为 ASCII 码字符。

```python
>>> ord('b')
98
```


## 小结 && 后记

本节记录了函数和模块，经典的海龟绘图，以及简单的数据类型转换。

个人觉得 Python 似乎不是我想象中那么难，但是知识点还是非常多的，可能我学其他语言的时候没这么认真。

至少海龟绘图是非常有趣的。

>Update 2020/3/26：添加了简单的数据类型转换