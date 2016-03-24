---
title: Python 100题第四部分（节选自61-100题）
date: 2013-02-18 20:33:09
tags: [python, 算法]
---

## 第68题
> 有n个整数，使其前面各数顺序向后移m个位置，最后m个数变成最前面的m个数

C语言可以用栈来实现，Python里可以用一种讨巧的方法来实现：
```python
lst = range(n)
print (lst*2)[m:m+l]
```
<!-- more -->

第69-82题大多是链表操作的题，这是数据结构的范畴了，推荐读一读这两本书：

1. Data Structures and Algorithms Using Python
2. Python Algorithms - Mastering Basic Algorithms in the Python Language

## 第83题
> 求0-7所能组成的奇数个数
```python
from itertools import product

count = len(filter(lambda x: x%2, range(8)))
for i in range(2, 9):
    for j in product(range(8), repeat=i):
        if j[0] > 0 and j[-1]%2:
            count += 1

print count
```
后面结构体的一些题目，用类来实现就行了。字符串，时间和文件操作的，都大同小异，就不赘述了。

至此，本系列文章告一段落。
