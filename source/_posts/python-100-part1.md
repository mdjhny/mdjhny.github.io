---
title: Python 100题第一部分（节选自1-20题）
date: 2013-02-15 10:00:25
tags: [python, 算法]
categories: python
---

## 第1题
> 有1、2、3、4个数字，能组成多少个互不相同且无重复数字的三位数？都是多少？

```python
# 这是常规解法，效率太低，不推荐使用
# for i in range(1,5):
#     for j in range(1,5):
#         for k in range(1,5):
#             if( i != k ) and (i != j) and (j != k):
#                 print i,j,k

from itertools import permutations
for i in permutations(range(1, 5), 3):
    print i
```

<!-- more -->

## 第5题
> 输入三个整数x,y,z，请把这三个数由小到大输出。

用经典的冒泡排序来实现：
```python
lst = []
for i in range(3):
    x = int(raw_input('integer:\n'))
    lst.append(x)

length = len(lst) - 1
for i in range(length, -1, -1):
    for j in range(i):
        if lst[j] > lst[j+1]:
            lst[j], lst[j+1] = lst[j+1], lst[j]
print lst
```

## 第11题
> 有一对兔子，从出生后第3个月起每个月都生一对兔子，小兔子长到第三个月后每个月又生一对兔子，假如兔子都不死，问每个月的兔子总数为多少？

兔子的规律为裴波那契数列1,1,2,3,5,8,13,21……经典的递归方法效率太低（多次重复递归调用），可以缓存之前的结果加快速度，下面是代码：
```python
def fib(n):
    dic = {1:1, 2:1}
    if n < 3:
        return dic.values()
    for i in xrange(2, n):
        dic.setdefault(i+1, dic[i-1]+dic[i])
    return dic.values()

print fib(100)
```

## 第14题
> 将一个正整数分解质因数。例如：输入90,打印出90=2×3×3×5。

原题给出的思路如下：
程序分析：对n进行分解质因数，应先找到一个最小的质数k，然后按下述步骤完成：

1. 如果这个质数恰等于n，则说明分解质因数的过程已经结束，打印出即可。
2. 如果n<>k，但n能被k整除，则应打印出k的值，并用n除以k的商,作为新的正整数你n,重复执行第一步。
3. 如果n不能被k整除，则用k+1作为k的值,重复执行第一步。

有如下代码：
```python
n = int(raw_input("input number:\n"))
print "n = %d" % n
for i in range(2,n + 1):
    while n != i:
        if n % i == 0:
            print str(i)+'*'
            n = n / i
        else:
            break
print "%d" % n
```
实际上这个算法效率太低，我们可以进一步优化：
```python
def factorize(n):
    '''来自http://www.math.utah.edu/~carlson/notes/python.pdf'''
    if n < 2:
        return '本函数仅适用于不小于2的正整数'
    d = 2
    factors = []
    while n%d == 0:
        factors.append(d)
        n /= d
    d = 3
    while n > 1 and d * d <= n:
        if not n % d:
            factors.append(d)
            n /= d
        else:
            d += 2
    if n > 1:
        factors.append(n)
    return '×'.join(map(str, factors))
```
即先用2除该数，然后用3, 5, 7……除。 算法中用到一点数论的知识：**`若n不是素数，则n必有一个因数i满足：i<sqrt(n)`**

## 第15题
> 利用条件运算符的嵌套来完成此题：学习成绩>=90分的同学用A表示，60-89分之间的用B表示，60分以下的用C表示。

Python没有三元条件运算符，我们可以用以下语法等价：

    result = 真值 if 条件为真 else 假值

这题答案就可以写成
```python
grade = 'A' if score>=90 else 'B' if score>=60 else 'C'
```
上面是最标准的写法，推荐使用它。另外还有两种三元表达式的等价方法，也列在下面：
```python
# 方法1
grade = score>=90 and 'A' or (score>=60 and 'B' or 'C')
# 方法2
grade = ('C', 'B', 'A')[(score>=90) + (score>=60)]
```

## 第17题
> 输入一行字符，分别统计出其中英文字母、空格、数字和其它字符的个数。

两种方法，一种用`ord`函数比较ASCII码值，另一种是用`string`模块的相关函数或属性，代码略
