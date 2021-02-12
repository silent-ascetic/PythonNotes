# 10.库、包、模块

模块就是就有某些完整功能且可供外界调用的py文件

## 导入模块

语法格式： `import moduleName` 或 `from moduleName import 模块中的函数、类、变量等（* 表示导入全部）`  
使用 `import` 导入模块，要通过模块名.模块内容的方式调用模块中的内容  
使用 `from ... import ...` 导入模块，可直接使用模块中的内容  
按照python语法规范，导入语句必须放在文件开头，但是什么时候使用什么时候导入程序不报错。 导入模块所在的py文件会被执行,然后执行之后的代码  
`import moduleName as name` 当模块名很长时为模块起一个别名，减少之后的工作量

```text
import sys
from json import dumps

s = {1:'2', 3:'4'}
print(sys.version)
dumps(s)
print(s)
```

## 自定义模块

根据模块的定义，自己写的具有完整功能的单个py文件就是一个模块

在自己定义的模块中定义 `__all__` 列表可以自定义别人可以导入的内容,只适用于 `import ... from *`  
示例：

```python
__all__ = ['m', 'show', 'A']

m = 3


def show():
    print(m)


def my():
    print('my')


class A:
    pass
```

## 包

存放模块的文件夹  
python解释器会将包含 `__init__.py` 文件的文件夹识别为一个包  
导入包时会运行 `__init__.py`  
`__init__.py` 文件内容：

```python
from . import moduleName
'''
表示从当前文件夹导入模块，可以写多个
导入了哪个模块，其他文件就能（只能）通过 `import moduleName` 导入该模块
'''
__all__ = ['moduleName']
'''
列表中包含那个模块名，其他文件就能（只能）通过 `from packageName import moduleName` 导入模块
当moduleName为*时，会导入__all__列表中的所有模块
'''
```

## 库

个人理解：  
由一个或多个功能相近的包或模块组成

