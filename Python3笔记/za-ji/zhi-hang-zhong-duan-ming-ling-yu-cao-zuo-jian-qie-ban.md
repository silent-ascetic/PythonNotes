# 执行终端命令与操作剪切板

## Windows系统

### 一 . 执行控制台指令方法

**例如打开QQ**

**1. 使用os库中的system函数**

```python
import os
os.system('start D:\\QQ\\QQ.exe')
'''如果不加start,打开QQ后控制台窗口不关闭，直到QQ关闭，控制台窗口才关闭
   一条os.system()语句执行完成控制台会关闭，所以当执行后续命令需要依赖前面的命令时，将多条命令写到一条          os.system()语句内，多条控制台命令用 && 连接'''
```

**2. 同样是os库中的**

```python
import os
# 返回输出结果
os.popen('start D:\\QQ\\QQ.exe')
```

### 二. 操作剪切板

**使用pyperclip库中的函数**

```python
import pyperclip
pyperclip.copy(123)
pyperclip.copy('添加到剪切板')
# 将传入的参数添加到剪切板，参数可以是数字或字符串
```

## Linux系统\(待整理\)

