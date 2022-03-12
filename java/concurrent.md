1.使用线程
```java
 ExecutorService executorService = Executors.newCachedThreadPool();
    WaitNotifyExample example = new WaitNotifyExample();
    executorService.execute(() -> example.after());
    executorService.execute(() -> example.before());
```


2.线程机制
Executor
Daemom
守护线程是程序运行时在后台提供服务的线程，不属于程序中不可或缺的部分。当所有非守护线程结束时，程序也就终止，同时会杀死所有守护线程。main() 属于非守护线程。在线程启动之前使用 setDaemon() 方法可以将一个线程设置为守护线程。
Sleep
sleep() 可能会抛出 InterruptedException，因为异常不能跨线程传播回 main() 中，因此必须在本地进行处理。线程中抛出的其它异常也同样需要在本地进行处理。
Yield
建议其他相同优先级的线程运行
3.中断
          调用一个线程的 interrupt() 来中断该线程，如果该线程处于阻塞、限期等待或者无限期等待状态，那么就会抛出 InterruptedException，从而提前结束该线程。但是不能中断 I/O 阻塞和 synchronized 锁阻塞。
          如果一个线程的 run() 方法执行一个无限循环，可以在循环体中使用 interrupted() 方法来判断线程是否处于中断状态，从而提前结束线程。
       
pool调用 Executor 的 shutdown() 方法会等待线程都执行完毕之后再关闭，但是如果调用的是 shutdownNow() 方法，则相当于调用每个线程的 interrupt() 方法。
如果只想中断 Executor 中的一个线程，可以通过使用 submit() 方法来提交一个线程，它会返回一个 Future<?> 对象，通过调用该对象的 cancel(true) 方法就可以中断线程。
4.互斥同步
第一个是 JVM 实现的 synchronized，而另一个是 JDK 实现的 ReentrantLock。
lock可中断，也可变成公平锁，可绑定多个条件对象
5.线程间的协作
join；a.join()原线程会等待a结束
wait，notify
wait是object方法，sleep是Thread的静态方法
wait期间会释放锁，sleep不会
await() signal() signalAll()
6.线程状态
start方法只是让线程就绪，并没有开始运行，运行的标志是run方法运行；但只运行run方法实则未开启线程
7.JUC-AQS
8.线程安全
不可变的对象一定是安全的

互斥同步（阻塞同步）:悲观锁:
无论共享数据是否真的会出现竞争，它都要进行加锁（这里讨论的是概念模型，实际上虚拟机会优化掉很大一部分不必要的加锁）
非阻塞同步：乐观锁
先进行操作，如果没有其它线程争用共享数据，那操作就成功了，否则采取补偿措施（不断地重试，直到成功为止）。

无同步方案
threadlocal
经典 Web 交互模型中的“一个请求对应一个服务器线程”（Thread-per-Request）的处理方式
9.锁优化
jvm对synchronized
自旋锁，锁粗化，轻量级锁，偏向锁
锁对象才能用wait和notify方法

多线程的时间算法：
直接定义一个数，让他随次数的增加增加

lock接口比synchronized块的优势是什么：
1.能够显示获取和释放所锁
2.方便地实现公平锁（先来先得，但是在大部分情况下，非公平锁的效率高）

wait哪等待哪唤醒；

