# 同步

    同步就是协同步调，按预定的先后次序进行运行。如:你说完，我再说。

    "同"字从字面上容易理解为一起动作

    其实不是，"同"字应是指协同、协助、互相配合。

    如进程、线程同步，可理解为进程或线程A和B一块配合，A执行到一定程度时要依靠B的某个结果，于是停下来，示意B运行;B依言执行，再将结果给A;A再继续操作。

## 互斥锁

应用场景：多个线程发生资源竞争
使用互斥锁可以实现线程同步。

### Lock

    threading模块中的Lock类用来实现互斥锁

**acquire**  
`acquire(blocking=True, timeout=-1)`

> 可以阻塞或非阻塞地获得锁。  
> 当调用时参数 blocking 设置为 True （缺省值），阻塞直到锁被释放，然后将锁锁定并返回 True 。  
> 在参数 blocking 被设置为 False 的情况下调用，将不会发生阻塞。如果调用时 blocking 设为 True 会阻塞，并立即返回 False ；否则，将锁锁定并返回 True。  
> 当浮点型 timeout 参数被设置为正值调用时，只要无法获得锁，将最多阻塞 timeout 设定的秒数。timeout 参数被设置为 -1 时将无限等待。当 blocking 为 false 时，timeout 指定的值将被忽略。  
> 如果成功获得锁，则返回 True，否则返回 False (例如发生 超时 的时候)。


**release**  

> 释放一个锁。这个方法可以在任何线程中调用，不单指获得锁的线程。  
> 当锁被锁定，将它重置为未锁定，并返回。如果其他线程正在等待这个锁解锁而被阻塞，只允许其中一个允许。  
> 在未锁定的锁调用时，会引发 RuntimeError 异常。  
> 没有返回值。

**locked**

> 如果获得了锁则返回真值。


**实例**
```py
from threading import Thread, Lock
import time

g_num = 0


def test1():
    global g_num
    for i in range(1000000):
        lock.acquire()
        g_num += 1
        lock.release()

    print("---test1---g_num=%d" % g_num)


def test2():
    global g_num
    for i in range(1000000):
        lock.acquire()
        g_num += 1
        lock.release()

    print("---test2---g_num=%d" % g_num)


lock = Lock()
p1 = Thread(target=test1)
p1.start()

p2 = Thread(target=test2)
p2.start()

time.sleep(2)
print("---g_num=%d---" % g_num)
```

```text
执行结果：
---test1---g_num=1851827
---test2---g_num=2000000
---g_num=2000000---

分析：
    test1函数执行完for循环后g_num的值必定大于1000000，因为test1运行时，test2也在运行。
```

```py
from threading import Thread, Lock
import time

g_num = 0


def test(num):
    global g_num
    for i in range(1000000):
        lock.acquire()
        g_num += 1
        lock.release()

    print(f"---线程{num}---g_num=%d" % g_num)


lock = Lock()
for _ in range(4):
    p = Thread(target=test, args=(_,))
    p.start()



time.sleep(10)
print("---g_num=%d---" % g_num)
```
```text
运行结果：
---线程0---g_num=1655382
---线程2---g_num=1989043
---线程1---g_num=1989393
---线程3---g_num=2000000
---g_num=2000000---

分析：
    同上个例子一样，先执行完的线程输出的g_num的值必定大于for循环的次数。
```

### 死锁

线程中的某个或多个锁无法解锁，程序陷入无限阻塞状态。
在给线程上锁时设置超时时间可以有效避免死锁。


## 多线程同步

例子：
```py
from threading import Thread, Lock
from time import sleep


class Task1(Thread):
    def run(self):
        while True:
            if lock1.acquire():
                print("------Task 1 -----")
                sleep(0.5)
                lock2.release()


class Task2(Thread):
    def run(self):
        while True:
            if lock2.acquire():
                print("------Task 2 -----")
                sleep(0.5)
                lock3.release()


class Task3(Thread):
    def run(self):
        while True:
            if lock3.acquire():
                print("------Task 3 -----")
                sleep(0.5)
                lock1.release()


#使用Lock创建出的锁默认没有“锁上”
lock1 = Lock()
#创建另外一把锁，并且“锁上”
lock2 = Lock()
lock2.acquire()
#创建另外一把锁，并且“锁上”
lock3 = Lock()
lock3.acquire()

t1 = Task1()
t2 = Task2()
t3 = Task3()

t1.start()
t2.start()
t3.start()
```
上例实现三个线程按一定顺序执行。

## 线程间通信

queue模块中的Queue类，用法同multiprocessing模块中的Queue。

