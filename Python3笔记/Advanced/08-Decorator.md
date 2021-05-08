# 装饰器

## 应用场景

在执行一个操做之前要执行另一个操作时可以用装饰器

* 引入日志
* 函数执行时间统计
* 执行函数前预备处理
* 执行函数后清理功能
* 权限校验等场景
* 缓存

## 创建装饰器

栗子
```py

def check(fun):
    def inner():
        print('-----检查-----')
        fun()
    return inner


def insert():
    print("--------------插入---------------")


@check
def delete():
    print("---------删除--------------")


# 装饰器原理
insert = check(insert)

insert()
delete()

# @check等价于insert = check(insert)
# @check就是装饰器
```

## 多装饰器

```py
#定义函数：完成包裹数据
def makeBold(fn):
    print('------1---------')

    def wrapped():
        print('------11---------')
        return "<b>" + fn() + "</b>"

    return wrapped


#定义函数：完成包裹数据
def makeItalic(fn):
    print('------2---------')

    def wrapped():
        print('------22---------')
        return "<i>" + fn() + "</i>"

    return wrapped


@makeBold
@makeItalic
def test():
    print("------------3-----------")
    return "hello world-3"


print(test())
# 相当于test = makeItalic(makeBold(test))
# test() 从里到外执行
```
三个或三个以上同理

## 装饰器执行时间

```py
def check(fun):
    print('---------装饰---------')
    def inner():
        print('-----检查-----')
        fun()

    return inner


@check
def delete():
    print("---------删除--------------")
```
运行上述代码可以知道装饰器是在定义被装饰函数时就运行了。

## 装饰有参函数

```py
# def check(fun):
#     def inner(a):
#         print('-----检查-----')
#         fun(a)

#     return inner


# 使用不定长参数来解决被修饰函数参数个数不一致情况
def check(fun):
    def inner(*args, **kwargs):
        print('-----检查-----')
        fun(*args, **kwargs)

    return inner


@check
def delete(a):
    print(f"---------删除{a}--------------")


@check
def insert(a, b):
    print(f"---------插入{a}和{b}--------------")


delete(8)
insert(1, 3)
```

## 装饰有返回值函数

```py
def check(fun):
    def inner(*args, **kwargs):
        print('-----检查-----')
        ret = fun(*args, **kwargs)
        print('---finish------')
        return ret
    return inner




@check
def add(a, b):
    return a + b


print(add(1, 2))
```

## 通用装饰器

有没有参数、返回值的函数都能修饰
```py
def check(fun):
    def inner(*args, **kwargs):
        ret = fun(*args, **kwargs)
        return ret
    return inner


@check
def test():
    print('----test----')


@check
def add(a, b):
    return a + b


print(add(1, 2))
print(test())
```

**注：**
* 没有return语句的函数返回值是 `None`，反正它有一个值，所以 `ret = fun(*args, **kwargs)` 就不会报错
* 对于`*args, **kwargs` 参数列表，可以传参也可以不传

## 带参装饰器

```py
def check(arg=None):
    def check(fun):
        def inner(*args, **kwargs):
            ret = fun(*args, **kwargs)
            return ret
        return inner
    return check


@check('sh')
def test():
    print('----test----')


# 不传参数时也要写括号
@check()
def add(a, b):
    return a + b


print(add(1, 2))
```


## 类装饰器

基础知识
```py
class Test(object):
    def __call__(self):
        print('test')


t = Test()
# 在类中定义了 __call__ 方法就可以通过以下方法调用它
t()
```

正题
```py
class Check(object):
    def __init__(self, fun):
        print('初始化')
        self.__fun = fun

    # 这样写是通用的
    def __call__(self, *args, **kwargs):
        return self.__fun(*args, **kwargs)


# 等价于 test = Check(test)
@Check
def test():
    print('----test----')


@Check
def add(a, b):
    return a + b


print(add(1, 2))
test()

```
