# 13.程序传参

程序接受来自程序外的参数

```python
import sys

print(sys.argv)
```

`sys.argv` 会接受在终端使用python命令运行程序时输入的程序名和之后的参数 例如：python -u test.py a b `sys.argv` 打印结果 \['test.py', 'a', 'b'\]

