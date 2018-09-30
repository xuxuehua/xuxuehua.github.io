---
title: "threading"
date: 2018-09-27 19:39
---


[TOC]


# threading

threading是python中专门用作多线程，常用类是Thread

提高一个程序中的执行效率





## threading.enumerate()

查看线程数



## threading.current_thread()

当前线程名称



## threading.Lock()

对修改全局变量的地方，需要加锁

```
gLock = threading.Lock()
gLock.acquire()
gLock.release()
```

```
import threading
import random
import time

gMoney = 1000
gLock = threading.Lock()
gTotalTimes = 10
gTimes = 0


class Producer(threading.Thread):
    def run(self):
        global gMoney
        global gTimes
        while True:
            money = random.randint(100, 1000)
            gLock.acquire()
            if gTimes >= gTotalTimes:
                gLock.release()
                break
            gMoney += money
            print('%s produced %d, remaining %d' % (threading.current_thread(), money, gMoney))
            gTimes += 1
            gLock.release()
            time.sleep(0.5)


class Consumer(threading.Thread):
    def run(self):
        global gMoney
        while True:
            money = random.randint(100, 1000)
            gLock.acquire()
            if gMoney >= money:
                gMoney -= money
                print('%s costs %d, remaining %d' % (threading.current_thread(), money, gMoney))
            else:
                if gTimes >= gTotalTimes:
                    gLock.release()
                    break
                print('%s consumer will cost %d, but remaining %d is not enough.' % (threading.current_thread(), money, gMoney))
            gLock.release()
            time.sleep(0.5)


def main():
    for x in range(5):
        t = Producer(name='Producer threading %d' % x)
        t.start()

    for x in range(3):
        t = Consumer(name='Consumer threading %d' % x)
        t.start()


if __name__ == '__main__':
    main()
```



## threading.condition()

Lock 上锁是很消耗CPU的行为，condition可以在没有数据的时候，处于一个阻塞的状态。一旦有合适的数据，可以使用notify相关的函数来通知其他处于等待状态的线程。



### acquire 

上锁



### release 

解锁



### wait

当前线程处于等待状态，并且会释放锁，可以被其他线程使用notify和notify_all函数唤醒

被唤醒后会继续等待上锁，上锁后继续执行下面的代码



### notify

通知某个正在等待的线程，默认是第一个等待的线程



### notify_all

通知所有正在等待的线程，并且不会释放锁。需要在release之前调用







## example

```
import threading
import time


class Listening(threading.Thread):
    def run(self):
        for i in range(3):
            print('Listening %s' % i)
            time.sleep(1)


class Writing(threading.Thread):
    def run(self):
        for i in range(3):
            print('Writing %s' % i)
            time.sleep(1)


def main():
    t1 = Listening()
    t2 = Writing()
    
    t1.start()
    t2.start()

if __name__ == '__main__':
    main()
```