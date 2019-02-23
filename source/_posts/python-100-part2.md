---
title: Python 100题第二部分（节选自21-40题）
date: 2013-02-16 13:22:22
tags: [python, 算法]
categories: python
---

## 第29题
> 给一个不多于5位的正整数，要求：一、求它是几位数，二、逆序打印出各位数字。

这个几乎不用思考，Python最适合干类似的活儿了：
```python
print len(str(12345))
print '12345'[::-1]
```
<!-- more -->

和c语言对比下：
```c
main( )
{
    long a, b, c, d, e, x;
    scanf("%ld", &x);
    a = x/10000;        /*分解出万位*/ 
    b = x%10000/1000;   /*分解出千位*/ 
    c = x%1000/100;     /*分解出百位*/ 
    d = x%100/10;       /*分解出十位*/ 
    e = x%10;           /*分解出个位*/ 
    if (a!=0) printf("there are 5, %ld %ld %ld %ld %ld\n",e,d,c,b,a);
    else if (b!=0) printf("there are 4, %ld %ld %ld %ld\n",e,d,c,b);
       else if (c!=0) printf(" there are 3,%ld %ld %ld\n",e,d,c);
          else if (d!=0) printf("there are 2, %ld %ld\n",e,d);
             else if (e!=0) printf(" there are 1,%ld\n",e);
}
```

## 第36题
> 求100之内的素数

判断一个正整数N是否为素数，常规的思路是用1到根号N范围内的正整数去除它，如果都除不尽则为素数，这个算法对比较大的整数比较吃力，我们知道除了2以外的正偶数都不是奇数，因此只需在奇数中寻找素数：
```python
def is_prime(n):
    if n < 2:
        return False
    if n == 2:
        return True
    if n%2 == 0:
        return False
    d = 3
    while (n > 1) and (d**2 <= n):
        if n%d == 0:
            return False
        d += 2
    return True

print filter(is_prime, range(101))
```
这题可以和第14题对照，参见本系列文章[第一部分](/2013/02/15/python-100-part1/)。

## 第37题
> 对10个数进行排序

原题提示用选择排序，我们用Python来实现选择排序算法：
```python
def selection_sort(lst):
    n = len(lst)
    for i in range(n - 1):
        min = i
        for j in range(i+1, n):
            if lst[min] > lst[j]:
                min = j
        lst[i], lst[min] = lst[min], lst[i]
    return lst
```

## 第40题
> 将一个数组逆序输出

最简单的当然是`lst[::-1]`，不过为了向C语言看齐，我们用笨办法（the hard way）来实现它：
首先分析一下算法：

    0 <——> -1（第0个和倒数第一个互换，以下类似）
    1 <——> -2
    2 <——> -3
    ……

不难推出一般公式：`lst[i] <——> lst[-i-1]`，于是有如下代码：
```python
lst = range(9)
m = len(lst) / 2
for i in range(m):
    lst[i], lst[-i-1] = lst[-i-1], lst[i]
print lst
```
注意当元素个数为奇数时，会多进行一次转换，即将最中间的数和它自己原地交换，这并不影响最终结果。
