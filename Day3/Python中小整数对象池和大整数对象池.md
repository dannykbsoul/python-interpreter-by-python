1. 小整数对象池

整数在程序中的使用非常广泛，Python为了优化速度，使用了小整数对象池， 避免为整数频繁申请和销毁内存空间。

Python 对小整数的定义是 [-5, 256] 这些整数对象是提前建立好的，不会被垃圾回收。在一个 Python 的程序中，无论这个整数处于LEGB中的哪个位置，

所有位于这个范围内的整数使用的都是同一个对象。同理，单个字母也是这样的。

In [1]: a=-5

In [2]: b=-5

In [3]: a is b
Out[3]: True

In [4]: a=256

In [5]: b=256

In [6]: a is b
Out[6]: True

In [7]: a=1000

In [8]: b=1000

In [9]: a is b
Out[9]: False

intern机制处理空格一个单词的复用机会大，所以创建一次，有空格创建多次，但是字符串长度大于20，就不是创建一次了。

In [13]: a="abc"

In [14]: b="abc"

In [15]: a is b
Out[15]: True

In [16]: a="helloworld"

In [17]: b="helloworld"

In [18]: a is b
Out[18]: True

In [19]: a="hello world"

In [20]: b="hello world"

In [21]: a is b
Out[21]: False

 

s1 = "abcd"
s2 = "abcd"
print(s1 is s2)

s1 = "a" * 20
s2 = "a" * 20
print(s1 is s2)

s1 = "a" * 21
s2 = "a" * 21
print(s1 is s2)

s1 = "ab" * 10
s2 = "ab" * 10
print(s1 is s2)

s1 = "ab" * 11
s2 = "ab" * 11
print(s1 is s2)
# True
# True
# False
# True
# False

 

2.大整数对象池。说明：终端是每次执行一次，所以每次的大整数都重新创建，而在pycharm中，每次运行是所有代码都加载都内存中，属于一个整体，所以

 这个时候会有一个大整数对象池，即处于一个代码块的大整数是同一个对象。c1 和d1 处于一个代码块，而c1.b和c2.b分别有自己的代码块，所以不相等。

C1.b is C2.b

In [22]: a=1000

In [23]: b=1000

In [24]: a is b
Out[24]: False

In [25]: a=-1888

In [26]: b=-1888

In [27]: a is b
Out[27]: False

In [28]: 

c1 = 1000
d1 = 1000
print(c1 is d1)  # True


class C1(object):
    a = 100
    b = 100
    c = 1000
    d = 1000


class C2(object):
    a = 100
    b = 1000


print(C1.a is C1.b)  # True
print(C1.a is C2.a)  # True
print(C1.c is C1.d)  # True
print(C1.b is C2.b)  # False

