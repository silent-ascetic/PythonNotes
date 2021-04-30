# 05.循环

## while循环

用法：

```py
a = 1
# 只此一种用法，a < 10可替换成其他表示真假值的语句
while a < 10:
    print(a)
    a += 1
```

## for循环

用法：

```python
a = 'qwert'
# 从变量a中依次取出一个元素赋到变量_中，a必须是可迭代类型
for _ in a:
    print(_)

# 第二种用法，不常用
for _ in a:
    if _ == 'e':
        break
else:
    print('循环正常结束')

'''
循环正常结束，即迭代完a中的所有元素后执行else下的代码
如果循环非正常结束，如执行了 `break` 语句，不会执行else下的代码
'''
```

