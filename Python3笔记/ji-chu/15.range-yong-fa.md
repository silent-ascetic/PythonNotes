# 15.Range用法

## 说明

**根据参数生成特定列表，最多传入三个参数：start、stop、step，stop无缺省值，start缺省值为0，step缺省值为1**  
**从start向stop取值，间隔为step，取值范围\[start, stop\)** **参数只能是整数，step为负数时从stop向start取值，间隔为step绝对值，取值范围同上** **python2中直接返回列表，如果列表过长会内存溢出， python3中返回一个range类的对象，用一个数，生成一个数，防止内存溢出,配合for循环使用** **python3中不接受关键字参数，即start=1，python2不知道，所以在python3中要设置step值，只能三个参数都传**

## 应用\(python3\)

```python
z = range(9)
print(z, type(z))
# 结果：range(0, 9) <class 'range'>

a = set()
z = range(2, -1, -1)
for i in z:
    a.add(i)
print(a)
# 结果：{0, 1, 2}

a = set()
z = range(2, 8, 2)
for i in z:
    a.add(i)
print(a)
# 结果：{2, 4, 6}
```

