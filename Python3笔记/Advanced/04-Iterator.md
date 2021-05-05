# 迭代器

### 迭代

迭代通俗讲就是循环遍历。

**可迭代类型：**  
字符串、字典、列表、元组、迭代器等可以通过 `for` 循环遍历的类型。

判断变量是否可迭代
```py
from collections.abc import Iterable
# from collections import Iterable   3.3版本以下

print(isinstance([], Iterable))
print(isinstance(100, Iterable))
```


可迭代不一定是迭代器，判断是否为迭代器方法如下
```py
from collections.abc import Iterator

print(isinstance([], Iterator))
```

## 创建迭代器

用 `iter` 函数可将**可迭代类型**创建为迭代器对象    
迭代器可以用 `next` 或 `__next__()` 函数进行迭代，
```py
it = iter("123456")
print(next(it))
print(it.__next__())
```

将创建迭代器类
```py
class Numbers:
  def __iter__(self):
    self.a = 1
    return self
 
  def __next__(self):
    x = self.a
    self.a += 1
    return x


num = MyNumbers()
myiter = iter(num)
print(next(myiter))
print(next(myiter))
```
