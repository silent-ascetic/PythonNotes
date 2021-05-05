# 作用域

> python搜索变量、函数等内容的顺序：locals -> enclosing -> globals -> builtin（局部->外部嵌套->全局->内置）

## 命名空间

某个范围的作用域，局部或全局都可以称作命名空间

## locals

使用locals函数可以查看当前局部作用域中所有变量、函数等。  
小栗子
```py
def test():
    a = 100
    def testIn():
        print('sssssssssss')
    print(locals())

test()
```

## enclosing

外部嵌套命名空间

## globals

查看全局中的变量、函数等

栗子
```py
def test():
    a = 100
    def testIn():
        print('sssssssssss')
    print(globals())

test()
print(locals())
print(globals())
```

## builtins

python解释器内建（内置）模块 `__builtins__`   
在Python启动后，且没有执⾏程序员所写的任何代码前，Python会⾸先加载该内建函数到内存。  
另外，该内建模块中的功能可以直接使⽤，不⽤在其前添加内建模块前缀。

查看 `__builtins__` 模块中内容
```py
print(dir(__builtins__))
```
> 低版本中可能是 `__builtin__`

导入该模块时用其引用名 `import builtins`
