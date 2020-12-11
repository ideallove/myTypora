---
layout: post
title: Re:从零开始的Python3学习笔记 05
date: 2020-04-27 11:00:00
description: <blockquote><h3><center>Python3 基础学习笔记（五）列表2</center></h3></blockquote><br/>
categories: 
- [Python学习笔记, 基础学习]
tags: 
- python
- 语言基础
cover: true
thumbnail: "https://cdn.idealx.cn/blogimage/python/python-icon.png"
permalink: python/basic-05.html
---

<blockquote><center>Python3 基础学习笔记（五） --  列表2</center></blockquote>

------

### - 3.2.6 排序列表元素

列表元素提供了 **`sort()`方法** 对列表进行排序。

> 排序（Sort），按照次序分为 增序 和 减序（又叫升序、降序）；增序一般根据 ASCII 码由小到大对字符、数字进行排序，减序则相反。

sort() 方法使用格式为 A.sort(key=none,reverse=False) .

>A 为列表对象
>
>key 为可选参数，默认值为 none，用于指定在做比较之前，调用何种函数对列表元素进行处理，比如 key=str.lower。
>
>reverse 为可选参数，默认为增序，使用reverse=True做减序处理。

示例：

```python
fruits = ['apple', 'banana', 'pear', 'peach', 'watermelon']
fruits_1 = fruits.copy()
fruits_2 = fruits.copy()
fruits_1.sort()
fruits_2.sort(reverse=True)
print(fruits_1)
print(fruits_2)
```

输出结果：

```python
['apple', 'banana', 'peach', 'pear', 'watermelon']
['watermelon', 'pear', 'peach', 'banana', 'apple']
```

> 如果不想改变原有列表，则可以采用 **sorted() 函数**，对列表对象直接排序。sorted 函数也可用于元组、字典的排序。

### - 3.2.7 复制列表

**copy() 方法**使用格式为 A.copy() 。通过 copy() 方法实现列表在内存里的复制（深拷贝）。

```python
fruits = ['apple', 'banana', 'pear', 'peach', 'watermelon']
fruits_1 = fruits.copy()
print(id(fruits))		# 打印列表的内存地址
print(id(fruits_1))
```

输出结果：

```python
3044623542152
3044632643272
```

> 如果是使用赋值号，则内存地址不变，是浅拷贝。

### - 3.2.8 统计列表元素

**count() 方法** 使用格式为 A.count(str) 。其中 str 为需要统计的元素。使用该方法实现对列表指定元素个数的统计。

```python
fruits = ['apple', 'banana', 'pear', 'peach', 'watermelon', 'peach']
x = fruits.count('peach')
print(x)
```

输出结果：

```python
2
```

### - 3.2.9 反向列表元素

**reserve() 方法** 使用格式为 A.reverse() 。通过该方法可以实现对列表元素的永久反向。

```python
text = [1, 2, 3, 4, 5]
print(text)
text.reverse()
print(text)
```

输出结果：

```python
[1, 2, 3, 4, 5]
[5, 4, 3, 2, 1]
```

> 列表做反向操作前后，列表对应的地址不变。

### - 3.2.10 列表解析

Python 语言还为列表提供了基于列表本身的元素操作语句解析功能。

> 语法如下：
>
> ```markdown
> [expression for iter_val in iterable]
> [expression for iter_val in iterable if cond_expr]
> ```

示例：对集合 0~10 中，除了 0 外，其他元素做平方运算。

```python
squares = [i ** 2 for i in range(11) if i > 0]
print(squares)
```

输出结果：

```python
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```

> 这样的写法，优点是简洁，缺点是调试不方便、写法不常见。

上述示例等价一般代码实现：

```python
squares = []
for i in range (1,11):
    squares.append(i ** 2)
print(squares)
```

### - 3.3 其他列表相关操作

列表的一些用法。

### - 3.3.1 遍历整个列表

使用 for 循环来遍历整个列表：

```python
fruits = ['apple', 'banana', 'pear', 'peach']
for fruit in fruits:
    print(fruit)
```

输出结果：

```python
apple
banana
pear
peach
```

### - 3.3.2 对数字列表执行简单的统计计算

使用**交互式解释器(IDLE解释器)**来理解 **`min函数、max函数、sum函数`** 。

```python
>>> nums = [1, 2, 3, 4, 5, 6, 7, 8, 9]
>>> min(nums)
1
>>> max(nums)
9
>>> sum(nums)
45
```

### - 3.4 后记

我码字的速度远远比不上我学习的速度......大概吧。