# 协程优点
* 主动让出CPU，程序控制切片。与线程不同，协程是自己主动让出CPU，并交付他期望的下一个协程运行，而不是在任何时候都有可能被系统调度打断。因此协程的使用更加清晰易懂，并且多数情况下不需要锁机制。
* 与线程相比，协程的切换由程序控制，发生在用户空间而非内核空间，因此切换的代价非常的小。
* 某种意义上，协程与线程的关系类似与线程与进程的关系，多个协程会在同一个线程的上下文之中运行，不需要锁	

## python 例子
```
import time

def comsumer():
    ret = ''
    while True:
        product = yield ret
        if not product:
            print("there is not any product")
            return
        print('[COMSUMER]: comsume %s '%product)
        time.sleep(1)
        ret = 'Done'

def produce(generator):
    generator.__next__() # 执行到yield处,返回的ret为null,无需获取
    n = 0
    while n < 10 :
        n += 1
        product = "prod" + str(n)
        print("[PRODUCT] product %s "% product) 
        ret = generator.send(product)
        print("[PRODUCT] result: %s"%ret)
    generator.close()

if __name__=='__main__':
    c = comsumer()
    produce(c)

```