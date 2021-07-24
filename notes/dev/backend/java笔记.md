# 多线程

**一、程序、进程、线程**

程序 静态的代码 

进程 正在运行的程序/程序的一次执行过程 、动态的 、资源分配的单位

线程 进程的进一步细化(360中同时进行体检、病毒查杀、磁盘扫描)	若一个进程可同时并行执行多个线程，就叫多线程、调度执行的单位，拥有独立的栈和程序计数器、多线程可以共享内存空间，完成通信，但同时也带来了安全隐患。

**二、单核CPU、多核CPU**

单核CPU——假的多线程，因为CPU的主频高所以感觉不出来

多核CPU——真正的多线程

一个java.exe程序至少有三个线程：main、异常处理线程、gc线程

**三、并行、并发**

并行——多个CPU同时执行多个任务。时间点

并发——一个CPU同时执行多个任务。时间间隔

**四、多线程**

优点：提高应用程序的响应增加用户体验、CPU的利用率、改善程序结构

何时需要：程序需要同时执行两个以上的任务，程序实现需要等待的任务：用户输入、文件读写、网络操作、搜索等，需要一些后台运行的程序

```java
/*
创建线程的方式一：定义一个线程类继承至Thread，重写run方法，main方法创建一个实例对象，调用start方法
start方法的两个操作：启动线程、调用run方法
注意1 如果直接调用run方法进行执行，则线程相当于没有被开启，只是相当于main中运行了一个普通的类方法
注意2 如果想创建多个线程，就创建多个thread对象 执行start即可
*/
class MyThread extends Thread{
    @Override
    public void run() {
        for(int i=0;i<100;i++){
            if(i%2==0){
                System.out.println(i);
            }
        }
    }
}
public class practice {
    @Test
    public void test1(){
        MyThread myThread = new MyThread();
        myThread.start();
    }
}
//使用匿名子类的方式启动新线程
				new Thread(){
            @Override
            public void run() {
                for(int i=0;i<100;i++){
                    if(i%2==0){
                        System.out.println(Thread.currentThread().getName()+":"+i);
                    }
                }
            }
        }.start();

/*
创建线程的方式二：实现Runnable接口，实现类重写Runnable接口的run方法，通过Thread类构造器创建线程对象，将Runnable接口的子类对象作为参数传递给Thread的构造器，调用Thread类的start方法
*/
class MyRunnable implements Runnable{
    @Override
    public void run() {
        for(int i=0;i<100;i++){
            if(i%2==0){              				 System.out.println(Thread.currentThread().getName()+":"+i);
            }
        }
    }
}
public class RunnableTest {
    public static void main(String[] args) {
        MyRunnable myRunnable = new MyRunnable();
        Thread t1 = new Thread(myRunnable);
        t1.start();
        Thread t2 = new Thread(myRunnable);
        t2.start();
    }
}
/*
继承方式和实现方式的区别
继承Thread:线程代码存放Thread子类run方法中。
实现Runnable:线程代码存在接口的子类的run方法。
实现方式的好处：避免了单继承的局限性，多个线程共享同一接口实现类的对象，适合多个相同线程来处理同一份资源   联想多窗口卖票  ticket不需要加static修饰
相同点：两种方式都需要重写run方法，线程执行的逻辑声明在run()中
*/
```

**五、Thread的常用方法**

```java
void start(): 启动线程，并执行对象的run()方法 
run(): 线程在被调度时执行的操作
String getName(): 返回线程的名称
void setName(String name):设置该线程名称
static Thread currentThread(): 返回当前线程。在Thread子类中就 是this，通常用于主线程和Runnable实现类
static void yield():线程让步
暂停当前正在执行的线程，把执行机会让给优先级相同或更高的线程
若队列中没有同优先级的线程，忽略此方法
join() :当某个程序执行(main)流中调用其他线程的 join() 方法时(mythread1)，调用线程(main)将被阻塞，直到 join()方法加入的join线程执行完为止
低优先级的线程也可以获得执行
static void sleep(long millis):(指定时间:毫秒)
令当前活动线程在指定时间段内放弃对CPU控制,使其他线程有机会被执行,时间到后 重排队。
抛出InterruptedException异常
stop(): 强制线程生命期结束，不推荐使用
boolean isAlive():返回boolean，判断线程是否还活着
```

**六、线程的调度和优先级**

调度策略：时间片轮转、抢占式

java的调度方法：同优先级的线程->先进先出->使用时间片轮转。高优先级采用抢占式。

```java
MAX_PRIORITY:10
MIN_PRIORITY:1
NORM_PRIORITY:5
getPriority()
setPriority(int newPriority)
//线程创建时继承父线程的优先级，低线程不一定非在高优先级线程执行完后再执行，只是获得调度的概率较低
```

**七、线程的分类**

守护线程：  服务用户线程、通过在start()方法前调用thread.setDaemon(true)可以把一个用户线程变成一个守护线程。

*Java垃圾回收就是一个典型的守护进程

*两者的唯一区别是判断JVM何时离开

*若JVM中都是守护线程，则当前JVM将退出

用户线程

**八、线程的生命周期**

![image-20210215104801285](/Users/alan/Library/Application Support/typora-user-images/image-20210215104801285.png)

**九、线程同步**

```java
//实现线程同步 方法一 ：同步代码块
class Window2 implements Runnable{
    private int ticket = 100;
    Object obj = new Object();
    @Override
    public void run() {
        while(true){
            //synchronized(this);最简单的方法，不需要创建一个新的对象，当前对象是唯一的，所以可以用 慎用
          	//synchronized(Window2.class) TO DO:Window2.class也是对象，只会加载一次，所以是唯一的
            synchronized (obj) {
                if (ticket > 0) {
                    System.out.println(Thread.currentThread().getName() + ":卖票,票号为" + ticket);
                    ticket--;
                } else {
                    break;
                }
            }
        }
    }
}
public class WindowTest {
    public static void main(String[] args) {
//        Window w1 = new Window();
//        Window w2 = new Window();
//        Window w3 = new Window();
//        w1.start();
//        w2.start();
//        w3.start();
        Window2 window2 = new Window2();
        Thread t1 = new Thread(window2);
        Thread t2 = new Thread(window2);
        Thread t3 = new Thread(window2);
        t1.setName("窗口1");
        t2.setName("窗口2");
        t3.setName("窗口3");
        t1.start();
        t2.start();
        t3.start();

    }
}
//方法二：同步方法
@Override
    public void run() {
        while(true){
            show();
        }
    }
    public synchronized void show(){
        synchronized (this) {
            if (ticket > 0) {
                try{
                    Thread.sleep(100);
                }catch (InterruptedException e){
                    e.printStackTrace();
                }
                System.out.println(Thread.currentThread().getName() + ":卖票,票号为" + ticket);
                ticket--;
            }
        }
    }
//方法三：使用Lock
class A{
	private final ReentrantLock lock = new ReenTrantLock(); 
  public void m(){
		lock.lock();
				try{
			//保证线程安全的代码;
				} finally{
        } 
 	 }
		}
Lock与synchronized的对比：
1. Lock是显式锁(手动开启和关闭锁，别忘记关闭锁)，synchronized是 隐式锁，出了作用域自动释放
2. Lock只有代码块锁，synchronized有代码块锁和方法锁
3. 使用Lock锁，JVM将花费较少的时间来调度线程，性能更好。并且具有更好的扩展性(提供更多的子类)
优先使用顺序:
Lock->同步代码块(已经进入了方法体，分配了相应资源)->同步方法 (在方法体之外)
```

**十、线程的通信**

wait()

Notify()

notifyAll()

**十一、创建线程的新方式**

![image-20210216104821848](/Users/alan/Library/Application Support/typora-user-images/image-20210216104821848.png)

![image-20210216105124422](/Users/alan/Library/Application Support/typora-user-images/image-20210216105124422.png)

![image-20210216105151914](/Users/alan/Library/Application Support/typora-user-images/image-20210216105151914.png)

# JUC

```java
//存在问题  多线程对同一变量i的访问i++存在问题
public class day03_09 {
    public static void main(String[] args) {
        myRunable2 my = new myRunable2();
        for(int i =0;i<20;i++){
            new Thread(my).start();
        }
    }
}
class myRunable2 implements Runnable{
    private int i = 0;
    public int getI(){
        return i++;
    }
    @Override
    public void run() {
        System.out.println(Thread.currentThread().getName()+"---"+getI());
    }
}

```

```java
output:
Thread-0---0//
Thread-6---4
Thread-5---3
Thread-4---2
Thread-3---1
Thread-1---0//
Thread-2---0//
Thread-10---8
Thread-11---9
Thread-9---7
Thread-8---6
Thread-7---5
Thread-13---11
Thread-12---10
Thread-14---12
Thread-15---13
Thread-16---14
Thread-17---15
Thread-18---16
Thread-19---17
```

```JAVA
//使用AtomicInteger原子类
import org.junit.Test;

import java.util.concurrent.atomic.AtomicInteger;

public class day03_09 {
    public static void main(String[] args) {
        myRunable2 my = new myRunable2();
        for(int i =0;i<20;i++){
            new Thread(my).start();
        }
    }

}

class myRunable2 implements Runnable{
    private AtomicInteger i = new AtomicInteger();
    public int getI(){
        return i.getAndIncrement();
    }
    @Override
    public void run() {
        System.out.println(Thread.currentThread().getName()+"---"+getI());
    }
}
Thread-0---0
Thread-5---5
Thread-4---4
Thread-3---3
Thread-2---2
Thread-1---1
Thread-8---8
Thread-9---9
Thread-7---7
Thread-6---6
Thread-10---10
Thread-11---11
Thread-12---12
Thread-13---13
Thread-14---14
Thread-15---15
Thread-16---16
Thread-17---17
Thread-18---18
Thread-19---19
```

```java
// CountDownLatch 闭锁
//闭锁：在完成某些运算时，只有其他所有线程的运算全部完成，当前运算才能继续执行
import java.util.concurrent.CountDownLatch;

public class testCountDownLatch {
    public static void main(String[] args) {
        final CountDownLatch latch = new CountDownLatch(5);
        long start = System.currentTimeMillis();
        thread th = new thread(latch);
        for(int i =0;i<5;i++){
            new Thread(th).start();
        }
        try {
            latch.await();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        long end = System.currentTimeMillis();
        System.out.println("执行结束，所用时间为:"+(end-start));
    }
}

class thread implements Runnable{
    private static CountDownLatch latch;
    public thread (CountDownLatch latch){
        this.latch = latch;
    }
    @Override
    public void run() {
        for(int i =0;i<50000;i++){
            if(i%2==0){
                System.out.println(i);
            }
        }
        latch.countDown();
    }
}

```

```java
//实现Callable接口的线程创建方式
import java.util.concurrent.Callable;
import java.util.concurrent.ExecutionException;
import java.util.concurrent.FutureTask;

public class testCallable {
    public static void main(String[] args) {
        thread1 td1 = new thread1();
        FutureTask<Integer> result = new FutureTask<>(td1);
        new Thread(result).start();
        try {
            Integer sum = result.get();
            System.out.println("============" + sum);
        } catch (InterruptedException | ExecutionException e) {
            e.printStackTrace();
        }
    }
}
class thread1 implements Callable<Integer> {

    @Override
    public Integer call() throws Exception {
        int sum = 0;
        for (int i = 0; i < 10000; i++) {
            sum += i;
            System.out.println(Thread.currentThread().getName() + " " + i);
        }
        return sum;
    }
}

```

