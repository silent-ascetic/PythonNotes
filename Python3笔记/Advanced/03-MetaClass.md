# 元类

python中一切皆对象，对象由类创建，而类则由元类创建。

type既是元类。type事实上是一个类，它能够创建其他类，程序中定义的类在运行时都是通过type来创建。

当然type()还可以返回变量的类型

我们也可以自己通过type来创建类
```py
# 类中的方法，类方法、静态方法等定义方式同在类中定义方式
def show(self):
    print(self.name)


@staticmethod
def Static():
    print("static method ....")


# 参数一：类名；参数二：父类（元组）；参数三：方法、类属性（字典）
A = type("className", (), {"show":show, "Static":Static "name":"petter"})
B = type("B", (A,), {})
a = A()
b = B()
a.show()
b.show()
# __class__属性存放对象所属的类
print(A.__class__, a.__class__)
```


**自定义元类**

类中的 `__metaclass__` 属性规定该类是由什么元类创建。  
python在内存中创建类之前会在该类、其父类、所在模块中寻找 `__metaclass__` 属性。  
如果有，则按照其值来创建类；如果没有，则用type来创建类。  
我们可以通过 `__metaclass__` 来实现使用自定义元类来创建类。

python2与python3中 `__metaclass__` 用法有所不同  

python2
```py
#-*- coding:utf-8 -*-
def upper_attr(future_class_name, future_class_parents, future_class_attr):

    #遍历属性字典，把不是__开头的属性名字变为大写
    newAttr = {}
    for name,value in future_class_attr.items():
        if not name.startswith("__"):
            newAttr[name.upper()] = value

    #调用type来创建一个类
    return type(future_class_name, future_class_parents, newAttr)

class Foo(object):
    __metaclass__ = upper_attr #设置Foo类的元类为upper_attr
    bar = 'bip'

# print(hasattr(Foo, 'bar'))
print(hasattr(Foo, 'BAR'))

f = Foo()
print(f.BAR)
```

python3

```py
class Foo(object, metaclass=upper_attr):
    bar = 'bip'

# print(hasattr(Foo, 'bar'))
print(hasattr(Foo, 'BAR'))

f = Foo()
print(f.BAR)
```

用一个真正的class来当做元类。
```py
class UpperAttrMetaClass(type):
    # __new__ 是在__init__之前被调用的特殊方法
    # __new__是用来创建对象并返回之的方法
    # 而__init__只是用来将传入的参数初始化给对象
    # 你很少用到__new__，除非你希望能够控制对象的创建
    # 这里，创建的对象是类，我们希望能够自定义它，所以我们这里改写__new__
    # 如果你希望的话，你也可以在__init__中做些事情
    # 还有一些高级的用法会涉及到改写__call__特殊方法，但是我们这里不用
    def __new__(cls, future_class_name, future_class_parents, future_class_attr):
        #遍历属性字典，把不是__开头的属性名字变为大写
        newAttr = {}
        for name,value in future_class_attr.items():
            if not name.startswith("__"):
                newAttr[name.upper()] = value

        # 方法1：通过'type'来做类对象的创建
        # return type(future_class_name, future_class_parents, newAttr)

        # 方法2：复用type.__new__方法
        # 这就是基本的OOP编程，没什么魔法
        # return type.__new__(cls, future_class_name, future_class_parents, newAttr)

        # 方法3：使用super方法
        return super(UpperAttrMetaClass, cls).__new__(cls, future_class_name, future_class_parents, newAttr)


class Foo(object, metaclass=UpperAttrMetaClass):
    bar = 'bip'


print(hasattr(Foo, 'BAR'))

f = Foo()
print(f.BAR)
```
