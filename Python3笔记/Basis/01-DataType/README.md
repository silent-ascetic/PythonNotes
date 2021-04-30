---
description: 数据类型总览
---

# 01.数据类型

**python中所有数据类型都是引用数据类型**

## 类型说明

1. [int](01.int.md)：整型
2. [float](02.float.md)：浮点型
3. [complex](03.complex.md)：复数
4. [bool](04.bool.md)：布尔类型
5. [str](05.str.md)：字符串
6. [list](06.list.md)：列表
7. [dict](07.dict.md)：字典
8. [tuple](08.tuple.md)：元组
9. [set](09.set.md)：集合

## 类型查看

可以使用`type()`来查看数值或变量的类型

```python
a = 'a'
print(type(a), type(4))
```

## 类型转换

举个栗子：

```python
a = str(3)
b = int('3')
c = (a, b)
d = list(c)
e = int(True)
f = bool('a')
# 错误写法
c = int('s')
```

**可迭代类型（列表、元组等）与不可迭代类型之间不可相互转换**

## 是否可以改变

可变类型：字典、列表、集合 不可变类型：数字、字符串、元组

## 是否可迭代

可迭代类型：字典、列表、元组、集合、字符串 不可迭代类型：数字

