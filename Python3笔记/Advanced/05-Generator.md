# 生成器

根据列表元素的生成算法循环生成元素的机制。  
生成器可以理解为存储列表元素生成算法的函数，它一次生成一个元素，可以有效减少内存占用，适用于数据庞大情况。  
生成器可以通过 `next` 函数来一个个取值，也可以迭代。它是一种特殊的迭代器。

## 创建方式

### 第一种方式

```py
# 列表
myList = [_ for _ in range(10)]

# 生成器
gen = (_ for _ in range(10))

print(myList)
print(gen)

for i in gen:
    print(i)
```

### 第二种

一个包含一个或多个 `yield` 关键字的函数就是生成器  
它返回的是一个生成器对象。

```py
def test1():
    for i in '123456':
        if i == '4':
            yield i


def test2():
    for i in range(1000000000):
        yield i


t1 = test1()
t2 = test2()

# 也可以用循环遍历
print(next(t1))
print(next(t2), t2.__next__(), next(t2))
```

**注：**
* 第一次 `next(t2)`，函数中代码会运行到 `yield i` 停住
* 第二次 `next(t2)`，函数中代码从 `yield i` 之后的代码再次运行到 `yield i`

**send**

`yield` 还可以接收 `send` 函数传递的参数
```py
def test():
    for i in range(20):
        tmp = yield i
        print(tmp)


t = test()

next(t) # 或 t.send(None)

print(t.send("第二次"))
print(t.send("第三次"))
```

**注：**  
第一次不能用send传值，会报错。
