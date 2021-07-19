# 异步


个人理解就是甲要做一件事，但是他要等乙完成某件事后才能做这件事。如果甲等着乙的期间什么都不做，就是安心等乙完事，这就叫同步；如果甲在等乙期间做另一个事情，等到乙完事后又放下现在正在做的事情去做一开始要做的事情，这就叫异步。

```py
from multiprocessing import Pool
import time
import os


def test():
    print("---进程池中的进程---pid=%d,ppid=%d--" % (os.getpid(), os.getppid()))
    for i in range(3):
        print("----%d---" % i)
        time.sleep(1)
    return "hahah"


def test2(args):
    print("---callback func--pid=%d" % os.getpid())
    print("---callback func--args=%s" % args)


if __name__ == '__main__':
    pool = Pool(3)
    # callback参数设置的是回调函数。
    pool.apply_async(func=test, callback=test2)

    while True:
        time.sleep(1)
        print("----主进程-pid=%d----" % os.getpid())
```
程序解析
    上边程序的执行逻辑是主进程等一个子进程完成后再继续运行，子进程完事要3秒，主进程却在循环打印，当子进程执行完后操作系统后会让主进程暂停现在在做的事而先执行子进程的回调函数（回调函数可以接受子进程的返回值）执行完回调函数后再继续执行主进程之前做的事。
