## Java中的多线程有三种实现方式：
1.   继承Thread类，重写run方法。Thread本质上也是一个实现了Runnable的实例，他代表一个线程的实例，并且启动线程的唯一方法就是通过Thread类的start方法。
2.   实现Runnable接口，并实现该接口的run()方法.创建一个Thread对象，用实现的Runnable接口的对象作为参数实例化Thread对象，调用此对象的start方法。
3.   实现Callable接口，重写call方法。Callable接口与Runnable接口的功能类似，但提供了比Runnable更强大的功能。有以下三点

> 1）. Callable可以在任务结束后提供一个返回值，Runnable没有提供这个功能。

> 2）. Callable中的call方法可以抛出异常，而Runnable的run方法不能抛出异常。

> 3）. 运行Callable可以拿到一个Future对象，表示异步计算的结果，提供了检查计算是否完成的方法。

_需要注意的是，无论用那种方式实现了多线程，调用start方法并不意味着立即执行多线程代码，而是使得线程变为可运行状态。_


## Java线程具有五中基本状态

* 新建状态（New）：当线程对象对创建后，即进入了新建状态，如：Thread t = new MyThread();

* 就绪状态（Runnable）：当调用线程对象的start()方法（t.start();），线程即进入就绪状态。处于就绪状态的线程，只是说明此线程已经做好了准备，随时等待CPU调度执行，并不是说执行了t.start()此线程立即就会执行；

* 运行状态（Running）：当CPU开始调度处于就绪状态的线程时，此时线程才得以真正执行，即进入到运行状态。注：就     绪状态是进入到运行状态的唯一入口，也就是说，线程要想进入运行状态执行，首先必须处于就绪状态中；

* 阻塞状态（Blocked）：处于运行状态中的线程由于某种原因，暂时放弃对CPU的使用权，停止执行，此时进入阻塞状态，直到其进入到就绪状态，才 有机会再次被CPU调用以进入到运行状态。根据阻塞产生的原因不同，阻塞状态又可以分为三种：
> 1. 等待阻塞：运行状态中的线程执行wait()方法，使本线程进入到等待阻塞状态；
> 2. 同步阻塞 -- 线程在获取synchronized同步锁失败(因为锁被其它线程所占用)，它会进入同步阻塞状态；
> 3. 其他阻塞 -- 通过调用线程的sleep()或join()或发出了I/O请求时，线程会进入到阻塞状态。当sleep()状态超时、join()等待线程终止或者超时、或者I/O处理完毕时，线程重新转入就绪状态。

* 死亡状态（Dead）：线程执行完了或者因异常退出了run()方法，该线程结束生命周期。