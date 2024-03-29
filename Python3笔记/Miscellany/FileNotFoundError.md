# 找不到文件错误

## 问题说明

**使用vscode编译python文件时报错`No such file or directory: 'img/0.png'`。即编译时无法正确找到文件路径**

## 源文件

```python
from PIL import Image
img = Image.open('img/0.png')
img.show()
```

**文件树：**

```
py
 └─test
      │  open.py
      │
      └─img
             0.png
```

## 问题分析

**产生错误的原因是运行open.py文件的终端所在目录不是open.py文件所在目录**

## 解决方法

1. 将vscode终端cd到py文件所在目录，如果用code runner插件，将运行py文件的命令改为`cd $dir && python -u $fileName`
2. 将文件路径改为绝对路径。（test文件夹位置改变就不行了）
3. 用代码获取当前文件的运行目录

```python
   f'{os.path.dirname(__file__)}/img/0.png'
   '''
   os.path.dirname(__file__)获取当前文件路径
   f'{os.path.dirname(__file__)}'表示将os.path.dirname(__file__)转译成它所表示的字符串
   '''
```

