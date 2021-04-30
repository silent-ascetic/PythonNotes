---
description: 数据类型总览
---

# 01.数据类型

**python中所有数据类型都是引用数据类型**

## 类型说明

1. [int](https://github.com/silent-ascetic/PythonNotes/tree/76479db272c4b8b3735dbb0824ed80cb047ccadf/Python3笔记/02-基础/数据类型/01.int.md)：整型
2. [float](https://github.com/silent-ascetic/PythonNotes/tree/76479db272c4b8b3735dbb0824ed80cb047ccadf/Python3笔记/02-基础/数据类型/02.float.md)：浮点型
3. [complex](https://github.com/silent-ascetic/PythonNotes/tree/76479db272c4b8b3735dbb0824ed80cb047ccadf/Python3笔记/02-基础/数据类型/03.complex.md)：复数
4. [bool](https://github.com/silent-ascetic/PythonNotes/tree/76479db272c4b8b3735dbb0824ed80cb047ccadf/Python3笔记/02-基础/数据类型/04.bool.md)：布尔类型
5. [str](https://github.com/silent-ascetic/PythonNotes/tree/76479db272c4b8b3735dbb0824ed80cb047ccadf/Python3笔记/02-基础/数据类型/05.str.md)：字符串
6. [list](https://github.com/silent-ascetic/PythonNotes/tree/76479db272c4b8b3735dbb0824ed80cb047ccadf/Python3笔记/02-基础/数据类型/06.list.md)：列表
7. [dict](https://github.com/silent-ascetic/PythonNotes/tree/76479db272c4b8b3735dbb0824ed80cb047ccadf/Python3笔记/02-基础/数据类型/07.dict.md)：字典
8. [tuple](https://github.com/silent-ascetic/PythonNotes/tree/76479db272c4b8b3735dbb0824ed80cb047ccadf/Python3笔记/02-基础/数据类型/08.tuple.md)：元组
9. [set](https://github.com/silent-ascetic/PythonNotes/tree/76479db272c4b8b3735dbb0824ed80cb047ccadf/Python3笔记/02-基础/数据类型/09.set.md)：集合

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

