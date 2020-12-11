---
layout: post
title: Re:从零开始的Python3学习笔记 03
date: 2020-04-06 17:40:00
updated: 2020-04-07 10:20:00
description: <blockquote><h3><center>Python3 基础学习笔记（三） -- 条件分支与循环</center></h3></blockquote><br/>本节记录了本节记录了if条件分支、while循环、for循环、break语句、continue语句等。
categories: 
- [Python学习笔记, 基础学习]
tags: 
- python
- 语言基础
cover: true
thumbnail: "https://cdn.idealx.cn/blogimage/python/python-icon.png"
permalink: python/basic-03.html
---
<blockquote><center>Python3 基础学习笔记（三） -- 条件分支与循环</center></blockquote>

------



## - 2 条件分支与循环

Python 语言的条件分支、循环使得代码内容具有了逻辑判断以及处理能力，如判断某个条件是真的还是假的，然后去执行不同的代码功能模块。这好比野外探险者，往山上走，结果会迷路；往山下走，会碰到提供帮助的人。不同的逻辑判断和选择，会产生不同的效果，在计算机编程上也是如此。程序员会把条件分支与循环语句结合数据，可以实现灵活而功能强大的各种代码算法。

> 在 Python 中的条件分支与循环语句，有着严格的缩进要求，这与其他语言使用的大括号不太一样。

### - 2.1 if 条件分支

if 语句是 Python 语言基本的条件分支判断语句，它为代码的逻辑判断提供了操作方法。

#### - 2.1.1 单分支判断

```python
if boolean_value1:
    子模块代码1
```

1）判断条件

`boolean_value1` 为 if 语句判断条件，以布尔值的形式判断 if 语句是否执行`子代码模块1`。当`boolean_value1` 值为 `True` 时，则执行`子代码模块1`；当值为 `False` 时，则不执行。

> 对于 `boolean_value1` ，除了直接采用布尔值外，还可以以表达式的形式体现，表达式计算最终结果为布尔值。

2）示例

```python
# 示例  
>>> if True:
    print('OK')
OK				# 结果
# 示例2
>>> if 2<5:
    print('YES')
YES				# 结果
```

> 说明：
>
> （1）if 语句的 “:” 冒号不能省略，并且要求是半角符号；
>
> （2）注意缩进，上述示例子模块代码中，必须先输入`4个空格`（或者 `Tab` 键），或者直接按`Enter` 接受默认换行。

####  - 2.1.2 双分支判断

```python
if boolean_value1:
    子模块代码1
else:
    子模块代码2
```

示例（运行 .py 程序，也可使用交互式解释器）：

```python
if False:			# 条件值为False
    print('YES')	# 不执行这一行
else:
    print('NO')		# 因此执行这一行
NO					# 结果
```

#### - 2.1.3 多条件多分支判断

```python
if boolean_value1:
    子模块代码1
elif boolean_value2:
    子模块代码2
else:
    子模块代码3
```

> elif 其实是else if的缩写（在Python中必须用elif）。
>
> 这里引入 elif 进行新的条件判断，在 if 语句中 elif 可以根据实际情况连续使用。但是else只能用在最后而且只能用一次。

```python
neko = '猫'
if neko == '狗':
    print('不是猫')
elif neko == '兔子':
    print('不是猫')
elif neko == '猪':
    print('不是猫')
else:
    print("是猫")
是猫	# 结果
```

> if 语句支持嵌套。

### - 2.2 while 循环

while 循环语句为程序员提供了循环处理算法的功能。

**1） while 语句基本用法**

```python
while boolean_value1:
    子模块代码1
```

这里使用简单流程图来说明：

```flow
st=>start: 开始
wh=>condition: while...条件循环
code=>operation: Code操作
en=>end: While结束

st->wh
wh(no)->en
wh(yes)->code->wh
```



**2）示例一**

```python
i = 0			# 循环控制变量i赋初值0
while i < 3:	# 当i小于3时，执行下面两行子模块代码
    i += 1		# i 做加1运算
    print(i)	# 打印输出i
1				# 第1次循环结构,i=1
2				# 第2次循环结构,i=2
3				# 第3次循环结构,i=3
```

> 与 if 语句一样，while语句也具备嵌套使用的功能。

**3）示例二（嵌套）**

```python
i,j = 0,6
while i<3:
    while i<j:
        print("%d"%((i+1)*j))
        j-=1
    i+=1		# 该行仅收到第1个while控制，通过缩进格式对其控制代码行范围
6
5
4
3
2
1
```

### - 2.3 for 循环语句

for 循环语句是 Python 语言的另外一种形式的循环控制语句。

**1）for 语句基本用法**

for 语句的基本语法格式如下：

```python
for <variable> in <sequence>:
    子模块代码1
else:
    子模块代码2
```

>variable 接受 sequence 集合中获取的成员元素，循环一次接受一次。

**2）示例1：利用自定义集合对象实现for循环**

```python
zhi_record = '一只羊、两只羊、三只羊、一头猪、两头猪、三头猪'
i = 0
for var in zhi_record:	# 循环一次var获取一个字符，一个汉字为一个双字节字符
    if var == '只':
        i = i + 1
        print(i)
1	# 找到第1个“只”字符
2	# 找到第2个“只”字符
3	# 找到第3个“只”字符
```

>该例把字符串当作集合，对所有字符进行了遍历比较，并把经过比较确认是“只”的字符个数进行统计，并打印输出

**3）示例2：利用内建范围函数 range 实现 for 循环**

```python
for i in range(9):			# range(9)为0~8的有序集合
    if i % 2 == 0:
        print('%d是偶数'%(i))
# 执行结果如下
0是偶数
2是偶数
4是偶数
6是偶数
8是偶数
```

**4）示例3：range函数的另外一种用法**

格式为 `range(start,stop[,step])`。start 代表数字的开始值，stop 代表数字的结束值，step 代表循环时数字递增的步长（默认值为1）。

```python
for i in range(1,9,2):
    print(i)
# 执行结果如下
1
3
5
7
```

### - 2.4 循环控制语句

在 while 和 for 循环过程中，为了更加灵活地控制循环次数，Python 提供了 break 和 continue 循环控制语句。

#### - 2.4.1 break 语句

break 语句可以立即终止并跳出循环。

```python
uw = 'Kirito,Alice,Eugeo,Asuna'
for i in range(len(uw)):
    print('for循环%d次'%(i+1))			# 检查循环次数
    if uw[i:i+6] == 'Kirito':			# 条件判断	
        print('Kirito is %d'%(i))
        break
    print('for循环继续吗？%d次'%(i+1))
# 执行结果
for循环1次
Kirito is 0
```

> 利用break语句，可以实现高效率的循环查找过程。
>
> break 语句适用于 while 和 for 语句。

#### - 2.4.2 continue 语句

continue 语句在满足条件的情况下回到循环开始处，继续循环，而忽略了continue后的语句。

```python
for i in range(9):
    if i % 2 != 0:
       continue
    print('%d为偶数'%(i))
# 运行结果
0为偶数
2为偶数
4为偶数
6为偶数
8为偶数
```

>continue 语句同样适用于 while 和 for 语句。
>
>实际编程中，continue 语句使用较少。

### - 2.5 复杂条件及处理

if、while和for控制的条件分支和循环分支，除了使用简单的变量、算数运算符、比较运算符、赋值运算符、逻辑运算符、位运算符外，还可以使用 成员运算符、身份运算符 进行参与逻辑判断，或者在上述基础上进行综合条件判断。

#### - 2.5.1 成员运算符

对于具有集合概念的对象如数字序列、字符串、列表、元组、字典，可以通过成员运算符进行快速判断，而且代码会显得非常简洁。

| **运算符** |                 **运算规则描述**                  |
| :--------: | :-----------------------------------------------: |
|     in     |  在指定序列中**找到**值，返回True，否则返回False  |
|   not in   | 在指定序列中**找不到**值，返回True，否则返回False |

示例：

```python
if 2 not in range(10):
    print('2不在集合里')
else:
    print('2在集合里')
2在集合里	# 结果
```

#### - 2.5.2 身份运算符

Python 代码在内存中运行时会生成各种各样的实体对象，如数字对象、字符串对象、列表对象、元组对象、字典对象等。通过身份运算符可以判断两个标识符（对象名）是否引用自同一个对象。若在内存中不同对象名指向的内存地址为同一个地址，那么它们是引用自一个对象。

| **运算符** |                       **运算规则描述**                       |
| :--------: | :----------------------------------------------------------: |
|     is     | 判断两个表示是不是引用自**一个对象**，是则返回True，否则返回False |
|   not is   | 判断两个表示是不是引用自**不同对象**，返回True，否则返回False |

```python
>>> a=b=1	# 为a和b赋值
>>> a is b	# 判断a和b是否引用同一对象
True
>>> c=1
>>> a is c
True
>>> c=2
>>> a is c
False
```

