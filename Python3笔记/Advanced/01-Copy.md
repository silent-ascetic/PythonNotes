# 深/浅拷贝

## 浅拷贝

拷贝地址


```py

a = {1:'q'}

b = a

```

## 深拷贝

通俗讲，新开辟一块内存用来存储原变量中的值，并用一个新变量来指向新内存。
通过 `copy` 模块实现深拷贝

可迭代类型变量存储可迭代类型元素时，存储的是它的地址。  
使用 `copy.deepcopy` 进行深拷贝时，会将其中的可迭代类型元素分别进行深拷贝，然后再将新的内存地址存储到新变量中。用 `copy.copy` 不会深拷贝可迭代类型元素，它只会将元素原地址添加到新变量中。


```py
import copy

a = [1, 3]

b = [a]

c = copy.deepcopy(a)

print(id(a), id(c))

e = copy.deepcopy(b)
f = copy.copy(b)
a.append(5)

print(b)
print(e)
print(f)
```

`copy.copy` 为不可变类型执行浅拷贝
