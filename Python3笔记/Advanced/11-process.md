# 进程

> 正在运行的程序

## 多任务

### 1. 概念

  同时进行多个操作，如一个人边吃饭边看电视边听歌。

### 2. 实现原理

    单核CPU：将要运行的程序放到一个队列中，队列中一个程序使用CPU极短时间后换下一个程序使用。切换速度极快，可以假装同时执行。具体调度算法：时间片轮转、优先级调度等。

    多核CPU：就是多个单核CPU，让每个CPU分别执行一个程序，如果还有多余程序就等下一批执行。原理同单核CPU。

### 3. 并发与并行

    并发：当要运行的程序多于CPU核数时，假装同时运行的状态
    并行：CPU核数大于等于要运行的程序数，真正同时运行的状态。

### 具体实现

python中os模块中的 `fork()` 函数可以创建一个子进程来实现多任务。只适用于Unix及其衍生系统。

#### 举例说明

例一：
```py
import os
import time

print("主进程")
id = os.fork()
for _ in range(100):
    print(f'运行次数{_}')
    time.sleep(1)

```

例二：
```py
import os
import time

print("主进程")
id = os.fork()
if id == 0:
  for _ in range(100):
      print(f'进程id:{id} 运行次数{_}')
      time.sleep(1)
else:
  for _ in range(100):
      print(f'进程id:{id} 运行次数{_}')
      time.sleep(1)
```
注：当主进程运行到 `id = os.fork()` 时会创建一个子进程来，子进程的id为0，父进程id大于零，两个进程同时运行。主进程创建子进程后也可以叫做父进程。

例三：
```py
import os

id = os.fork()
if id == 0:
    print(f'id:{id}**pid{os.getpgid()}**(父)ppid{os.getppid()}')
else:
    print(f'id:{id}**pid{os.getpgid()}')
```
注：父进程的id值为子进程的pid， ppid为父进程的pid

例四：
```py
import os
import time

id = os.fork()
if id == 0:
    print("子进程")
    time.sleep(1)
    print('子进程结束')
else:
    print('父进程')
```
注：父进程与创建出来的子进程是两个独立的进程。比如说夫亲和儿子是两个独立的人。

