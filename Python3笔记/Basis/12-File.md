# 12.文件操作

用python对其他文件进行操作

## 打开/关闭文件

```python
# 打开文件
file = open('filePath', 'openMode')
# 关闭文件
file.close()
'当文件/夹与程序在同一目录，可直接用文件/夹名'
```

openMode详解：

r：只读模式，只能读取文件，不能写入。文件不存在会报错  
w：写入模式，只能写入不能读取，文件不存在自动创建，文件存在清空文件内容再写入  
a：追加模式，只能写入不能读取，在文件末尾追加内容，文件不存在自动创建  
r+/w+/a+：可读可写并保留r、w、a模式特点  
rb/wb/ab：以二进制方式进行r、w、a操作  
rb+/wb+/ab+：同上

默认打开模式为r

## 文件指针

同用文本编辑器打开文件时光标的功能，标识从哪个地方读取或写入内容。

关于文件指针的操作：

```python
file = open('filePath')
'''
将文件指针移动到指定位置
a表示移动几个字符
b表示从哪里开始移动，0：文件开头，1：指针当前位置，2：文件结尾
'''
file.seak(a, b)
# 返回文件指针位置
file.tell()
```

## 读文件

```python
file = open('filePath', 'r')
# file = open('filePath')
# 读取文件所有内容并返回为字符串(有数字参数时表示读取几个字符)
file.read()
# 读取一行内容并返回(有数字参数时表示读取一行中的几个字符，参数超出改行总共字符数时返回改行内容)
file.readline()
# 按行读取文件内容并保存到列表中
file.readlines()
```

## 文件操作常用函数

### os模块

```python
import os

# 删除文件
os.remove('filePath')
# 删除空文件夹
os.rmdir('folderPath')

'''递归删除目录。工作方式类似于 rmdir()，不同之处在于，如果成功删除了末尾一级目录，removedirs() 会尝试依次删除 path 中提到的每个父目录，直到抛出错误为止（但该错误会被忽略，因为这通常表示父目录不是空目录）。例如，os.removedirs('foo/bar/baz') 将首先删除目录 'foo/bar/baz'(必须是空文件夹)，然后如果 'foo/bar' 和 'foo' 为空，则继续删除它们。如果无法成功删除末尾一级目录，则抛出 OSError 异常。'''
os.removedirs('folderPath')

# 创建文件夹
os.mkdir('folderPath')

# 重命名文件
os.rename('oldName', 'newName ')

# 判断是文件还是文件夹
os.path.isfile("path")
os.path.isdir('path')

# 判断是否为绝对路径
os.path.isabs('path')

# 判断文件（夹）是否存在
os.path.exists('path')

# 返回一个目录的目录名和文件名
os.path.split('path')

# 分离扩展名
os.path.splitext("path")

# 获取路径名
os.path.dirname('path')

# 获取文件名
os.path.basename('path')



# 将文件夹中的所有文件/夹名存储到列表中并返回
os.listdir('folderPath')

# 获取此脚本运行路径
os.getcwd()

# 更改默认路径(默认为程序运行路径)
os.chdir('path')
```

