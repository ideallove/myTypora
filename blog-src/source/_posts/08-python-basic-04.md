---
layout: post
title: Re:从零开始的Python3学习笔记 04
date: 2020-04-21 18:00:00
description: <blockquote><h3><center>Python3 基础学习笔记（四） -- 列表与操作列表</center></h3></blockquote><br/>
categories: 
- [Python学习笔记, 基础学习]
tags: 
- python
- 语言基础
cover: true
thumbnail: "https://cdn.idealx.cn/blogimage/python/python-icon.png"
permalink: python/basic-04.html
---

<blockquote><center>Python3 基础学习笔记（四） -- 列表与操作列表</center></blockquote>

------

### - 3.1 列表

**列表（List）**是由一系列按特定顺序的元素组成，在 Python 中用方括号 `[]` 来表示列表，并用逗号来分隔其中的元素。类似其他语言中的“数组”，但有一些区别。

> 列表是 Python 语言显著区别于其他语言的一种数据结构，其设计更具灵活性，可以弥补字符串本身的各种缺陷。

### - 3.1.1 列表基本知识

**使用`交互式解释器`**理解列表：

```python
>>> []				# 空列表
[]
>>> list1 = []		# 定义空列表
>>> len(list1)		# 列表长度（元素个数）:len()函数
0					# list1 的长度为 0
>>> list2 = [1,2]	# 定义列表
>>> len(list2)
2
>>> print(list2)	# 输出列表
[1, 2]
```

> **`len()` 函数** 可以快速获得列表的长度，经常在循环语句中使用。

列表的不同数据类型元素成员:

```python
>>> test1 = [1,2,3,4]		# 列表元素全为数字类型
>>> len(test1)
4
>>> test2 = ['a','b','c']	# 列表元素全为字符串
>>> len(test2)
3
>>> test3 = [10,20,'x','y']	# Python 列表元素支持综合类型
>>> len(test3)
4
>>> print(test3)
[10, 20, 'x', 'y']
>>> test4 = ['ABC', test1]	# Python 列表元素也可以列表
>>> len(test4)
2
>>> print(test4)
['ABC', [1, 2, 3, 4]]
```

和大部分语言一样，Python 列表的**下标（索引）**也是从 0 开始的。

```python
list1 = ['a','b','c','d','e']
print(list1[0])		# 第一个元素
print(list1[3])
print(list1[-1])	# Python 支持倒过来找。
print(list1[-2])
# 结果:
a
d
e
d
```

### - 3.1.2 列表切片操作

```python
list = [1,2,3,4,5,6]
print(list[:])		#省略全部，代表截取全部内容，可以用来将一个列表拷给另一个列表
print(list[:3])		#省略起始位置的索引，默认起始位置从头开始，结束位置索引为2
print(list[3:])		#省略结束位置的索引，默认结束位置为最后一个，开始位置索引为3
print(list[1:4])	#开始位置索引为1，结束位置索引为3，顾头不顾尾
print(list[4:1])	#从左到右索引，因此为空值
print(list[-1:-3])	#从左到右索引，因此为空值
print(list[-3:-1])	#开始位置索引为倒数第三个，结束位置索引为倒数第二个
print(list[1:5:2])	#开始位置索引为1，结束位置索引为4，间隔2
print(list[5:1:-1])	#反向取值，开始位置索引为5，结束位置索引为2
print(list[::-1])	#反向取值，反向输出列表
```

输出结果：

```python
[1, 2, 3, 4, 5, 6]
[1, 2, 3]
[4, 5, 6]
[2, 3, 4]
[]
[]
[4, 5]
[2, 4]
[6, 5, 4, 3]
[6, 5, 4, 3, 2, 1]
```

### - 3.1.3 使用列表中的元素

方法 `title()` 可以像使用其他变量一样使用列表中的各个值。

```python
list_test = ['C', 'C++', 'Java', 'Python', 'php', 'JavaScript']
message = list_test[4].title() + "是世界上最好的语言!(雾)"
print(message)
```

输出结果

```python
Php是世界上最好的语言!(雾)
```

### - 3.2 列表基本操作 ---- 组织列表

在创建的列表中，元素的排列顺序常常是无法预测的。Python 提供了很多组织列表的方式，可根据具体情况使用。

列表支持对集合元素进行增加、查找、修改、删除、合并操作等。

| 方法名称 |         方法功能描述         |
| :------: | :--------------------------: |
|  append  |      在列表尾部增加元素      |
|  clear   |           列表清空           |
|   copy   |     复制生成另外一个列表     |
|  count   |       统计指定元素个数       |
|  extend  |       两个列表元素合并       |
|  index   |      返回指定元素的下标      |
|  insert  |     在指定位置插入新元素     |
|   pop    | 删除并返回指定下标对应的元素 |
|  remove  |      删除列表中指定元素      |
| reverse  |       反转列表元素顺序       |
|   sort   |      对列表元素进行排序      |

### - 3.2.1 添加列表元素

列表提供 `append()` 方法和 `insert()` 方法添加列表元素。

**（1）方法 `append()`** ：在列表末尾添加元素。

```python
list = [1, 2, 3, 4, 5, 6]
print(list)
list.append(7)
print(list)
```

输出结果：

```python
[1, 2, 3, 4, 5, 6]
[1, 2, 3, 4, 5, 6, 7]
```

**（2）方法`insert()`**：在列表指定位置添加元素

```python
fruits = ['apple', 'banana', 'peach']
print(fruits)
fruits.insert(0,'watermelon')
fruits.insert(1, 10)
print(fruits)
```

输出结果：

```python
['apple', 'banana', 'peach']
['watermelon', 10, 'apple', 'banana', 'peach']
```

### - 3.2.2 查找列表元素

列表可以通过 **`index()` 方法**、in成员运算符、下标、切片查找相应的元素信息。

这里这里使用 **交互式解释器** 理解 index() 方法。（当然直接写.py程序是一样的，交互式解释器可以更好地理解方法的运行方式。）

**`index()` 方法**使用格式为 **`A.index(value,[start[,stop]])`**。其中，A 是列表对象，value 代表需要在列表 A 查找的元素，start 代表在列表里开始查找的下标数，stop 则代表查找结束的下标数，中括号代表 start、stop 是可选的参数。若查到元素，则会返回第一个找到的元素；若未查找到元素，则会返回错误信息。

```python
>>> listx = ['alice', 1, 2, 4, 1]
>>> listx.index('alice')	# 在列表里查找
0							# 返回列表下标 0
>>> listx.index(1)
1
>>> listx.index(1,2)		# 从下标 2 开始查找元素1
4							# 返回下标 4
>>> listx.index(10)			# 查找数字10，返回错误信息
Traceback (most recent call last):
  File "<pyshell#13>", line 1, in <module>
    listx.index(10)
ValueError: 10 is not in list
```

> 如果 **不在** *交互式解释器* 中的话，index() 方法输出需要写成类似 `print(listx.index(1))` 的输出结果哦。

### - 3.2.3 修改列表元素

列表可以通过指定下标，对相对应的元素进行赋值修改。

与字符串相比，列表元素具有可修改的特点，使其获得了巨大的操作灵活性。

```python
listx = [1, 2, 3, 'alice']
print(listx)
listx[0] = 'underworld'
print(listx)
```

输出结果：

```python
[1, 2, 3, 'alice']
['underworld', 2, 3, 'alice']
```

### - 3.2.4 删除列表元素

**（1）`clear()` 方法**：清除列表对象里的所有元素，列表对象变成空列表

```python
fruits = ['apple', 'banana', 'peach']
print(fruits)
print(len(fruits))
fruits.clear()
print(fruits)
print(len(fruits))
```

结果如下：

```python
['apple', 'banana', 'peach']
3
[]
0
```

**（2）`pop()` 方法**

pop() 方法可以弹出并删除最后一个元素，或者弹出指定下标的元素。

**1、使用 pop() 方法删除最后一个元素**

pop() 的无参方法可以删除列表末尾的元素，并能够接着使用它。术语 **弹出（pop）**源自这样的类比：列表就像是一个栈，而删除列表末尾的元素就相当于弹出栈顶元素：

```python
fruits = ['apple', 'banana', 'peach', 'watermelon', 'banana']
print(fruits)
new_list = fruits.pop()
print(fruits)
print(new_list)
```

输出结果：

```python
['apple', 'banana', 'peach', 'watermelon', 'banana']
['apple', 'banana', 'peach', 'watermelon']
banana
```

**2、使用 pop() 方法删除指定位置的元素**

pop([index]) 指定参数来删除指定位置的元素。

```python
fruits = ['apple', 'banana', 'peach', 'watermelon', 'banana']
print(fruits)
new_list = fruits.pop(2)	# 指定列表下标 2
print(fruits)
print(new_list)
```

输出结果：

```python
['apple', 'banana', 'peach', 'watermelon', 'banana']
['apple', 'banana', 'watermelon', 'banana']
peach
```

**（3）`remove()` 方法**：删除未知位置的元素

当我们不知道元素的位置，只知道元素的值的时候，可以使用该方法。

```python
fruits = ['apple', 'banana', 'peach', 'watermelon', 'banana']
print(fruits)
fruits.remove('banana')
print(fruits)
```

输出结果：

```python
['apple', 'banana', 'peach', 'watermelon', 'banana']
['apple', 'peach', 'watermelon', 'banana']
```

> 注意：remove() 方法与index() 方法类似，只能查找到第一个。

**（4）`del` 函数**

Python 语言里的 del 函数具有强大的对象删除功能，它也可以用来删除列表里指定的元素，甚至把整个列表对象删除。

```python
fruits = ['apple', 'banana', 'peach', 'watermelon', 'banana']
print(fruits)
del(fruits[4])	# 删除下标为 4 的元素
print(fruits)
del fruits		# 删除列表对象
print(fruits)
```

输出结果：

```python
['apple', 'banana', 'peach', 'watermelon', 'banana']
['apple', 'banana', 'peach', 'watermelon']
Traceback (most recent call last):
  File "C:\Users\ideallove\Desktop\pythontest2.py", line 6, in <module>
    print(fruits)
NameError: name 'fruits' is not defined
```

> 从以上举例可以知道，一旦元素或列表对象被删除，它的内存地址将会被回收，无法继续使用。

### - 3.2.5 合并列表元素

**（1）`extend()` 方法**：将两个列表对象合并

```python
listx = [1, 2, 3, 4, 5]
fruits = ['apple', 'banana', 'peach', 'watermelon', 'banana']
listx.extend(fruits)
print(listx)
```

输出结果：

```python
[1, 2, 3, 4, 5, 'apple', 'banana', 'peach', 'watermelon', 'banana']
```

**（2）使用运算符**

```python
listx = [1, 2, 3, 4, 5]
fruits = ['apple', 'banana', 'peach', 'watermelon', 'banana']
print(id(listx))	# 获取打印合并前的内存地址
listx = listx + fruits
print(id(listx))	# 获取打印合并后的内存地址
print(listx)
```

输出结果：

```python
1832405460296
1832405461384
[1, 2, 3, 4, 5, 'apple', 'banana', 'peach', 'watermelon', 'banana']
```

> 采用运算符合并赋值的方法，会使合并后的列表在内存中的地址号改变，这说明列表合并后被重新定义了（更换了列表对象）。
>
> 但是extend()方法不会更改内存地址号。
>
> 两种方法都可以达到合并的结果。
