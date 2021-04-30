# 06.逻辑判断

python中判断语句只有if（和while循环），不支持switch

判断数值相等或不等用 `==` 和 `!=`，用 `None` 表示空，`is` 比较地址

`==` 可以比较列表、元组、字典中的元素是否相等



## 与或非

### 逻辑与（and）

相当于C语言中的 `&&`  
举个栗子：

```py
print(True and False)
```

### 逻辑或（or）

相当于C语言中的 `||`  
举个栗子:

```py
print(True or False)
```

### 逻辑非（not）

类似C语言中的 `!`，`not` 后面可以接表示真假的表达式或变量表示非真或非假，但不能与等号连用 例如：

```py
print(not 1 == 3)
```

**知识点待完善**

## if用法

```py
if 's' in 'asf':
    print('666')
```

```py
if 3 == 4:
    print('haha')
else:
    print(666)
```

```py
if False:
    pass
elif False:
    pass
elif False:
    print('无限套娃')
else:
    print('结束了')
```

