# 09.类与对象

python中一切皆对象，定义的类也是对象，称为类对象。

## 语法规范

一个文件中可以定义多个类。类与类之间，类与其他代码之间要隔两行

## 类的组成部分

1. 类名
2. [方法](01.Method.md)
3. [属性](02.Attribute.md)

## 类定义与实例化

```python
class A:
    pass


a = A()
```

## 对象与对象引用

对象：通过 `className()` 实例化出来的具体对象  
对象引用：指向某对象所在内存地址的变量  
一个对象可以有多个对象引用，一个对象引用只能指向一个对象

示例：

```python
class A:
    pass


a = A()
b = a
c = a
```

## 销毁对象

1. python解释器的垃圾回收机制会自动销毁无用对象
2. 通过 `del objectName` 手动销毁对象
   * 此方法删除的是对象引用，当某对象的所有引用都被删除之后该对象才会被销毁
   * 获取某对象引用指向的对象有多少个对象引用 `sys.getrefcount(objectName)`，使用此方法时会新生成一个对象引用

示例：

```python
import sys
class A:
    pass


a = A()
b = a
c = a
print(sys.getrefcount(b))
del c
print(sys.getrefcount(b))
```

