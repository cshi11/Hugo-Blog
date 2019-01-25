+++
date = "2016-11-05T19:41:01+05:30"
title = "Python 基本语法"
writer = "子适"
draft = false
image = "img/portfolio/pylogo.jpg"
showonlyimage = false
categories = [ "code"]
weight = 2
description = "Individual meta description for this post"
+++

## 一、基本语法

### 1.1 输出

- 保留格式输出
<!--more-->

```python
print('''朝辞白帝彩云间
千里江陵一日还''')
```

- 占位符写法

| 占位符 | 替换内容   |
| ------ | ---------- |
| %d     | 整数       |
| %f     | 浮点数     |
| %s     | 字符串     |
| %x     | 十六进制数 |

```python
print("My name is %s" % "Shi")
```

- 固定输出格式

```python
s1 = 72
s2 = 85
delta = (s2 - s1) / s1
print("提升了 %.1f %%" % (delta * 100))
print("%.2f" % 3.2313)
```

### 1.2 List 和 Tuple

- List —— 有序集合

| 函数                | 功能             |
| ------------------- | ---------------- |
| len(list)           | 长度             |
| max(list)/min(list) |                  |
| list(seq)           | 元组转化为列表   |
| cmp(list1, list2)   | 比较两个列表元素 |

| 方法                                        | 功能             |
| ------------------------------------------- | ---------------- |
| list.append(obj)                            | 末尾添加元素     |
| List.count(obj)                             | 统计元素次数     |
| List.extend(seq)                            | 末尾追加新序列   |
| List.index(obj)                             | 找出索引         |
| List.insert(index, obj)                     | 插入             |
| list.pop([index = 1])                       | 移除             |
| List.remove(obj)                            | 移除第一个匹配项 |
| list.reverse()                              | 反转列表元素     |
| list.sort(cmp=None, key=None, reverse=False | 排序             |



```python
classmates = ['bob', 'tony', 'shi', 'hally']
// 删除元素
classmates.pop(1)
// 增加元素于末尾
classmates.append('pony')
print(classmates[0])
// 长度
print(len(classmates))
// 判断元素存在
print('pony' in classmates)
// 遍历
for student in classmates:
    print(student)
//拼接
print([1, 2, 3] + [4, 5, 6])
```

- List Comprehensions 列表生成

```python
L = list()	# 空列表
L = ['']*4	# ['', '', '', '']
```

```python
L = list(range(1, 11))
L1 = [x * x for x in range(1, 11)]
L2 = [x * x for x in range(1, 11) if x % 2 == 0]
L3 = [m + n for m in 'ABC' for n in "abc"]	//['Aa', 'Ab', 'Ac', 'Ba', 'Bb', 'Bc', 'Ca', 'Cb', 'Cc']
d = {'x': 'A', 'y': 'B', 'z': 'C'}
L4 = [k + '=' + v for k, v in d.items()]	// ['x=A', 'y=B', 'z=C']
```

- 列表和字符串转化

```python
L = list(str)	# str 转 list
s = ''.join(L)	# list 转 str
```



- Tuple —— 元组，一旦初始化无法修改。安全，尽量使用。

```python
t = (1,)	//只含一个元素时，需要这样写
// 下面的例子中，元组内的List的内容被改变了，但 tuple 未变，因为 List 地址不变
tt = (1, 2, [3, 4])
tt[2][0] = 19
print(tt)
```

- 切片（都适用）

```python
L = ['Michael', 'Sarah', 'Tracy', 'Bob', 'Jack']
L[0:3]
L[-2:]	//['Bob','Jack']
L = list(range(100))
L[:10:2]	// 前十个数，每两个取一个
// 字符串也适用
'ABCDEFG'[::2]	// 'ACEG'
```

### 1.3 dict & set

- Dict —— 储存键值对

```python
d = {'mike': 97, 'bob': 87, 'tracy': 99}
print(d['mike'])
print(d.get('mike', -1))	// get() 方法如果key不存在，返回 none，或者可以指定返回值
d.pop('bob')
```

- Set —— 不重复的集合
  - set 中不能保存可变元素，比如 list ,可以保存 tuple

```python
s = set()	//创造一个空 set
s = set([1,2,3])	// 需要list作为输入
s.add(4)
s.remove(4)
s1 & s2 	// 两个set可以做交集，并集
// 删除一个 list 中的重复元素
l = list(set(l))
```

### 1.4 str

- str 是不可变量

```python
a = 'abc'
print(a.replace('a', 'A'))	//Abc
print(a)	// abc

```

- Str 相关方法

  - 判断两个字符串相等 引入operator 模块

  ```python
  import operator as op
  op.eq('12','12')	// true
  
  ```

  

### 1.5 变量类型

- 局部变量
- 全局变量
- 类型变量
- 实例变量

### 1.6 基本运算

- `/` 就是除法，两个`int` 相除结果也是小数。地板除用`//`
- 幂运算 `**`

### 1.7 基本语法

- 循环

  ```python
  for i in range(5):
      ...
  # 如果用不到 i，只是单纯的循环5次，用 _
  for _ in range(5):
  ```

  

## 二、函数

### 2.1 函数定义 & 默认参数 & 可变参数

- 默认参数

```python
// 计算幂函数
def power(x, n=2):
    s = 1
    while n > 0:
        s = s * x
        n = n - 1
    return s
```

- 可变参数 *

```python
// 计算任意数的和
def calc(*numbers):
    summ = 0
    for x in numbers:
        summ += x * x
    return summ

print(calc(1, 2, 3))
lis = [1, 2, 3]
print(calc(*lis))  # 传入list时，在前面加 *
```

- 关键字参数 **

```python
def person(name, age, **kw):
    print('name:', name, 'age:', age, 'other:', kw)
    
>>> person('Michael', 30)
name: Michael age: 30 other: {}
            
>>> person('Bob', 35, city='Beijing')
name: Bob age: 35 other: {'city': 'Beijing'}
>>> person('Adam', 45, gender='M', job='Engineer')
name: Adam age: 45 other: {'gender': 'M', 'job': 'Engineer'}
```

- 命名关键字参数

```python
// 只接受 city 和 job 作为关键字参数
def person(name, age, *, city, job):
    print(name, age, city, job)
```



### 2.2 map & reduce

- `map()`函数接收两个参数，一个是函数，一个是`Iterable`，`map`将传入的函数依次作用到序列的每个元素，并把结果作为新的`Iterator`返回。

```python
// 对 list 中元素平方
>>> def f(x):
...     return x * x
...
>>> r = map(f, [1, 2, 3, 4, 5, 6, 7, 8, 9])
>>> list(r)
[1, 4, 9, 16, 25, 36, 49, 64, 81]
```

```python
// 将数字转化为字符，str 是函数
// 不加list 返回一个 map 对象，可以用于遍历，但不可视
>>> list(map(str, [1, 2, 3, 4, 5, 6, 7, 8, 9]))
```

```python
# 元组转 list
d = {(1,2), (3,4)}	# set 中只能装不变的对象，不能直接放入list
d_list = list(map(list, d))
[[1,2],[3,4]]

```



- `reduce`把一个函数作用在一个序列`[x1, x2, x3, ...]`上，这个函数必须接收两个参数，`reduce`把结果继续和序列的下一个元素做累积计算。

```python
from functools import reduce
reduce(f, [x1, x2, x3, x4]) = f(f(f(x1, x2), x3), x4)

```

- 综合案例

```python
DIGITS = {'0': 0, '1': 1, '2': 2, '3': 3, '4': 4, '5': 5, '6': 6, '7': 7, '8': 8, '9': 9}


def str2int(s):
    def fn(a, b):
        return a * 10 + b

    def str2num(ch):
        return DIGITS[ch]

    return reduce(fn, map(str2num, s))


print(str2int('39201'))
```

### 2.3 filter

- `filter()`也接收一个函数和一个序列。和`map()`不同的是，`filter()`把传入的函数依次作用于每个元素，然后根据返回值是`True`还是`False`决定保留还是丢弃该元素。

```python
def not_empty(s):
    return s and s.strip()

list(filter(not_empty, ['A', '', 'B', None, 'C', '  ']))
# 结果: ['A', 'B', 'C']
```

### 2.4 sorted

```python
sorted(iterable, key, reverse)
```

- 其中，`key`可以指定按照什么排序，`reverse = True`可以反向排序

```pytho
// 按照绝对值
>>> sorted([36, 5, -12, 9, -21], key=abs)
[5, 9, -12, -21, 36]
// 按照小写排序
>>> sorted(['bob', 'about', 'Zoo', 'Credit'], key=str.lower)
['about', 'bob', 'Credit', 'Zoo']
```

### 2.5 返回函数

### 2.6 匿名函数 lambda

```python
def is_odd(n):
    return n % 2 == 1

L = list(filter(is_odd, range(1, 20)))
L_lambda = list(filter(lambda x: x % 2 == 1, range(1, 20)))
```

### 2.7 装饰器 Decorator

- 不改变函数内部而给函数增加新功能，“装饰”一下。

```python
@log	//等价于加了一条语句 now = log(now)
def now():
    print('2019-8-2')
    
def log(func):
    def wrapper(*args, **kw):
        // .__name__ 方法可以拿到函数名字
        print('call %s():' % func.__name__)
        return func(*args, **kw)
    return wrapper

//执行
>>> now()
call now():
2015-3-25

```

### 2.8 枚举 Enumerate

- 遍历数据并计数

```python
my_list = ['apple', 'banana', 'grapes', 'pear']
for c, value in enumerate(my_list, 1):	// 第二个参数决定从几开始计数
    print(c, value)
# 输出:
(1, 'apple')
(2, 'banana')
(3, 'grapes')
(4, 'pear')
```

- 创建包含索引的元祖列表

```python
my_list = ['apple', 'banana', 'grapes', 'pear']
counter_list = list(enumerate(my_list, 1))
# [(1, 'apple'), (2, 'banana'), (3, 'grapes'), (4, 'pear')]
```



## 三、 高级特性

### 3.1 生成器 generator

- 只储存算法，不存数据，需要那个数据根据算法再去计算。因此理论上可以存储无限元素。

```python
 g = (x * x for x in range(10))	// 区分列表生成器 []
 // 取g值
 next(g)
 // 或者
for n in g:
    print(n)

```

- 一个函数如果包含 `yield` 关键字，它就是一个 generator

```python
// fib 数列
def fib(max):
    n, a, b = 0, 0, 1
    while n < max:
        a, b = b, a + b  # 交换
        n = n + 1
        yield a
    return 'done'


print(fib(8))	//<generator object fib at 0x10bc084f8>
for x in fib(8):
    print(x)

```

## 四、面向对象 OOP

### 4.1 类和实例

- 创建类和实例
  - 类中变量命名
    - 不加下划线——普通变量，外部可以通过 .name 访问
    - 前面加单下划线——保护变量，应视作私有变量使用
    - 前面加双下划线——私有变量，仅可通过内部方法访问
    - 前后加双下划线—— `__init__`  是特殊变量，可以访问

```python
class Student(object):	// object 是该类继承的类
     def __init__(self, name, score):        
        self.__name = name
        self.__score = score #变量名前加双下划线，变为私有变量
        
     def get_name(self):    # 私有变量仅可通过内部函数访问
        return self.__name

     def get_score(self):
        return self.__score

Bob = Student('Bob', 98)
print('%s : %d' % (Bob.get_name(), Bob.get_score()))
```




