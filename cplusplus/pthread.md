# pthread

## Summary

pthread(Portable Operating System Interface)定义了一套创建和操作线程的API.

Pthreads API中大致共有100个函数调用，全都以"pthread_"开头，并可以分为四类：

* `线程管理`, 例如`创建`线程, `等待`(join)线程, `查询`线程状态等。
* `互斥锁`(Mutex): 创建, 摧毁, 锁定, 解锁, 设置属性等操作
* `条件变量`(Condition Variable): 创建, 摧毁, 等待, 通知, 设置与查询属性等操作
* 使用了互斥锁的线程间的`同步`管理

POSIX的SemaphoreAPI可以和Pthreads协同工作, 但这并不是Pthreads的标准. 因而这部分API是以"sem_"打头, 而非"pthread_".
因为经常一起用所以也需要了解一下.

## Data Types

```cpp
pthread_t thread_name;  // pthread_t表示线程句柄

```

## Reference
