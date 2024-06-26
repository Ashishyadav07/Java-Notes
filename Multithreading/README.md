# Multithreading

## Difference between Multitasking, Mutliprocessing and Multithreading

### Multitasking

- Multitasking refers to the ability of a computer system to execute multiple tasks or processes concurrently.

- It increase the performance of the CPU.

![alt text](image.png)

- Two ways by which we can achive multiprocessing.
  - Process based Multitasking(MP)
  - Thread based Multitasking(MT)

### Multiprocessing

- When one system is connected to multiple processor in order to complete the task.

![alt text](image-1.png)

- It is best suitable at system level or OS level.

### Multithreading

- Executing multiple threads(sub process) at single time.

![alt text](image-2.png)

- Multi-threading is best suitable at programming level.

- It is mainly used in softwares, games and animation.

- JAVA provide pre-defined API for multi-threading.

  - Thread
  - Runnable
  - Thread Group
  - Concurrency
  - Thread Pool

Example

```java

VLC ( process, program )

class VLC
{
     public static void main(String[] args)
        {
               Video vid = new Video();
               vid.playvideo();
               Music mus = new Music();
               mus.playmusic();
        }
}

class Video   //Thread 1
{
      void playvideo()
          {
              //implementation
          }
}

class Music  //Thread 2
{
      void playmusic()
          {
              //implementation
          }
}

```

## Difference between process and thread.

### Process

- A program which is in executing state.
- Process is heavy weight because it contains thread also.
- Process takes more time in context switching(A context switching is a process that involves switching of the cpu from one process to another. In this phenomenon, the execution of the process that is present in the running state is suspended by the kernel and another process that is present in the ready state is executed by CPU)
- It takes more time in interprocess communication.
- Each process has different address space.
- Process are not dependent on each other.
- Process does not require Synchronization.
- Process consume more resource.
- Process takes more time for creation.
- Process require more timem for temination.

### Thread

- It is a subpart of a program.
- Thread is light weight.
- Context switching takes less time.
- It takes less time in interthread communication.
- Thread share same address space.
- Thread are dependent on each other.
- Thread may require Synchronization.
- Thread consume less resource.
- Thread require less time for creation.
- Thread require less time for termination.

## Thread life cycle. How to create threads?

There are two ways to create thread.

- Thread(class)
- Runnable(Interface)

Thread is a predefined class created by java which is in java.lang package. It consists of constructor and methods.

```java
class Thread{
    //constructor
    //method
    run();
    start();
    sleep();
    join();
    getName(); and setName();
    interrupted priority
    daemon
}
```

Examples of Constructor and methods in thread class.

![alt text](image-3.png)

![alt text](image-4.png)

![alt text](image-5.png)

### Steps to create thread.

```java
//Step 1: Extends the thread class
class Test extends Thread{
    //Step 2: Override the run method
    public void run(){
        //thread task
    }
    public static void main(String args[]){
        //Step 3: Create an object of the class
        Test t = new Test();
        //Step 4: Start the thread using start() method
        t.start();

    }
}
```

### Thread life cycle.

![alt text](image-6.png)

**New**

- When a thread object is created using new keyword, it is in a state that is called ‘New’ state. At this moment, only an object is created in the JVM. Please note that the thread hasn’t started working yet.

**Runnable**

- Remember the statment t.start(); ? We used this to start a thread, right? So, does the thread start when this method is called on it? The answer is no. start() method call only ensures that the thread is registered in a pool of threads which is refered by the Thread scheduler to run a particular thread.

- This thread pool is called Runnable pool, and the threads which are there in this pool are known to be in Runnable state.

- In this state, thread is runnable, meaning it can be picked up by the thread scheduler to run any time. But the thread is still not running.

**Running**

- A thread is said to be in this state when the thread is actully running its run() method code.

**Blocked/Waiting/Sleeping**

- A thread which is running can be pushed to one of the three states: Blocked/Waiting/Sleeping.

- Blocked state is the one in which a thread is blocked for some resource or a lock which is already acquired by another thread.

- Waiting state is the one in which a thread goes after calling wait() method.

- Sleeping state is the one in which a thread goes after calling sleep() method.

- All these 3 states are clubbed as one state because they are more or less similar. In any of these states, the thread is not eligible for running.

Note -> Once a thread goes back from any of these states, it doesn’t start running immediately. Rather it goes back to runnable pool of threads where it is upto the scheduler when that thread will be picked to run.

**Terminated or Dead**

- A thread goes to Terminated or Dead state when it completes its run() method execution. Once dead, a thread cannot be run again. If someone tries to start a dead thread, then an IllegalThreadStateException is thrown.

## How to create thread using Thread class and Runnable interface.

There are two ways by which we can create thread:

- Thread(Class)
- Runnable(Interface)

Thread class

- It is in package.java.lang
- It consist of many constructor and method.
- Thread class implements runnable interface.

```java
class Thread implements Runnable{
    //constructor
    //method
    run();

}

```

**Example**

```java
//Step 1: Extends the thread class
class Test extends Thread{
    //Step 2: Override the run method
    public void run(){
        System.out.println("Thread task");//thread task
    }
    public static void main(String args[]){
        //Step 3: Create an object of the class
        Test t = new Test();
        //Step 4: Start the thread using start() method
        t.start();
        //We cant invoke the start() method again.

    }
}
```

Runnable Interface

- It is in package.java.lang package.
- It consist of only one method which is run().

```java
public interface Runnable{
    //method
    run()
}
```

**Example**

```java
//Step 1: Implements the runnable interface
class Test implements Runnable{
    //Step 2: Override the run() method.
    public void run(){
        System.out.println("Thread task");//Thread task
    }
    public static void main(String args[]){
        //Step 3: Create an object of Test class
        Test t = new Test();
        //Step 4: Create an object of thread class and pass referce of test class in it.
        Thread th = new Thread(t);
        //Step 5: Invoke the thread.
        th.start();
    }
}
```

## Differenct cases of executing thread in java.

**1. Performing single task from single thread.**

```java

class Test extends Thread{
    public void run(){
        System.out.println("Thread task");//thread task
    }
    public static void main(String args[]){
        Test t = new Test();//Created one thread to execute one thread task
        t.start();
    }
}

```

**2. Performing single task from multiple thread.**

```java

class Test extends Thread{
    public void run(){
        System.out.println("Thread task");//thread task
    }
    public static void main(String args[]){//this is the main thread created by JVM.
        Test t = new Test();//thread 1
        t.start();
        Test t2 = new Test();//thread 2
        t2.start();
        //2 thread to perfom one task
    }
}

```

**3. Performing multiple task from single thread**

It is not possible because one thread can perform one task only.

**4. Performing multiple task from multiple thread**

```java
class MyThread1 extends Thread{
    public void run(){
        System.out.println("Thread1");//Task 1
    }
}
class MyThread2 extends Thread{
    public void run(){
        System.out.println("Thread2");//Task 2
    }
}
class Test{
    public static void main(String args[]){
        MyThread1 t1 = new MyThread1();//Thread 1
        t1.start();
        MyThread2 t2 = new MyThread2();//Thread 2
        t2.start();
        //All the thread gets executed simultaneously
    }
}
```

## Thread class methods and constructor.

### Thread constructor.

**Basic constructor**

- Thread()
- Thread(Runnable target)
- Thread(String name)
- Thread(Runnable target,String name)

**ThreadGroup constructor**

- Thread(ThreadGroup tg, Runnable target)
- Thread(ThreadGroup tg, String name)
- Thread(ThreadGroup tg, Runnable target, String name)
- Thread(ThreadGroup tg, Runnable target, String name, long stackSize)

### Thread methods.

**Basic Method**

- public void run(): is used to perform action for a thread.
- public void start(): starts the execution of the thread.JVM calls the run() method on the thread.
- public Thread currentThread(): returns the reference of currently executing thread.
- public boolean isAlive(): tests if the thread is alive.

**Naming Method**

- public String getName(): returns the name of the thread.
- public void setName(String name): changes the name of the thread.

**Daemon thread Method**

- public boolean isDaemon(): tests if the thread is a daemon thread.
- public void setDaemon(boolean b): marks the thread as daemon or user thread.

**Priority based method**

- public int getPriority(): returns the priority of the thread.
- public int setPriority(int priority): changes the priority of the thread.

**Preventing thread execution method**

- public void sleep(long miliseconds): Causes the currently executing thread to sleep (temporarily cease execution) for the specified number of milliseconds.
- public void yield(): causes the currently executing thread object to temporarily pause and allow other threads to execute.
- public void join(): waits for a thread to die.
- public void join(long miliseconds): waits for a thread to die for the specified miliseconds.

**Depreceated Method**

- public void suspend(): is used to suspend the thread(depricated).
- public void resume(): is used to resume the suspended thread(depricated).
- public void stop(): is used to stop the thread(depricated).

**Interrupting the thread method**

- public void interrupt(): interrupts the thread.
- public boolean isInterrupted(): tests if the thread has been interrupted.
- public static boolean interrupted(): tests if the current thread has been interrupted.

**Inter thread communication method**

![alt text](image-7.png)

## Programs of methods of Thread class.

**Program 1**

```java
public class ThreadNameDemo{
    public static void main(String args[]){
        System.out.println("Hello");
        System.out.println(Thread.currentThread().getName());//Output- main
        Thread.currentThread().setName("Ashish");
        System.out.println("New Thread Name " + Thread.currentThread().getName());//Ashish
        System.out.println(10/0);//Output - Exception in thread "Ashish" java.lang.ArithmeticException: / by zero
   }
}
```

**Program 2**

```java
public class Test extends Thread{
    public void run(){//thread - 0
        System.out.println("Thread task : " + Thread.currentThread().getName());//Thread - 0
        //Ashish
    }
    public static void main(String args[]){//main thread
        System.out.println("Hello : " + Thread.currentThread().getName());//main
        Test t1 = new Test();
        t1.start();
        Test t2 = new Test();
        t2.setName("Ashish");
        t2.start();
    }
}
```

## Daemon thread

- Daemon threads are low-priority threads that run in the background.
- It provides services to the user thread.
- It performs background operations such as garbage collection, finalizer, Action Listeners, Signal dispatches, etc.
- Example - Spelling checker in ms word which run in the backgroud and check spelling of the word.

**Methods**

- public final void setDaemon(boolean b) - It is used to set the thread as daemon
- public final boolean isDaemon() - It checks whether the thread is daemon or not

**Program 1**

```java
class Test extends Thread{
    public void run(){
        System.out.println("Child Thread");
    }
    public static void main(String args[]){
        System.out.println("Main method");//without this line the daemon thread will not run as daemon thread provide service to the main thread so if this line does not exist there will be nothing to execute in the main method so there is no need of daemon method.
        Test t = new Test()
        t.setDaemon(true);
        t.start();
    }
}

```

**Important point to remember**

- We have to create daemon thread before starting the thread, If we create daemon thread after starting it, it will throw runtime exception i.e IllegalThreadStateException.

- We cannot create main thread as daemon thread because because the main thread will be created and started by JVM and if you would like to mark it as a daemon thread you have to write the below line inside the main method, that means the thread already started hence it will throw the above exception.

- It's life depend on another thread.

- It inherit the properties from its parent thread. For example - If a thread is created by another thread and the parent thread is a daemon, the child thread inherits this status. However, if the parent thread is not a daemon, you need to explicitly mark the thread as a daemon.

- Daemon threads are not essential for the JVM to continue running. If the only threads executing are daemon threads, the JVM may decide to terminate them, which means daemon threads can't be relied upon for critical tasks.

- By default priorties of daemon thread is low.

## Thread Priorities

- JVM provides the priority to each thread and according to these priorities JVM allocates the processor.

- Priorites are represented in the form of integer values which ranges from 1 to 10.

  - 1 - MIN_PRIORITY
  - 5 - NORM_PRIORITY
  - 10 - MAX_PRIORITY

- Methods:
  - public final void setPriority(int value)
  - public final int getPriority()

```java
public class Test extends Thread{
    public void run(){
        System.out.println("Thread task");
        System.out.println("Child thread new priority"+Thread.currentThread().getPriority());//It will inherit the priority of main thread which is 10
    }
    public static void main(String args[]){
        System.out.println("Main thread old priority "+Thread.currentThread().getPriority());//by default priority of main thread is 5
        Thread.currentThread().setPriority(10);
        System.out.println("Main thread new priority "+Thread.currentThread().getPriority());
        Test t = new Test();
        t.start();
    }
}
```

**Important point to remember**

- Priorities are inherited from parent thread.
- By default main thread priority is 5.
- If priority value is not between 1 to 10 then it will throw runtime exception i,e IllegalArgumentException.
- If multiple thread priorities is same then we cant assume which will get executed firstly and lastly. It is handled by JVM algorithm.
- Windows don't support priorities.

## sleep() method.

- The sleep() method is a static method of Thread class and it makes the thread sleep/stop working for a specific amount of time.
- The sleep() method throws an InterruptedException if a thread is interrupted by other threads, that means Thread.sleep() method must be enclosed within the try and catch blocks or it must be specified with throws clause.

**Methods**

- public static native void sleep(long milliseconds) throws Interrupted Exception
- public static void sleep(long milliseconds, int nanoseconds) throws Interrupted Exception.

**Program 1**

```java
class Test{
    public static void main(String args[]){
        for(int i = 1; i <= 5; i++){
            try{
                Thread.sleep(1000);//Main thread will go in sleep mode for 1 sec every time loops get executed.
                System.out.println(i);
            }
            catch(Exception e){
                System.out.println(e);
            }
        }
    }
}
```

**Program 2**

```java
class Test extends Thread{
    public void run(){
        for(int i = 1; i <= 5; i++){
            try{
                Thread.sleep(1000);//Main thread will go in sleep mode for 1 sec every time loops get executed.
                System.out.println(i);
            }
            catch(Exception e){
                System.out.println(e);
            }
        }
    }
    public static void main(String args[]){
        Test t = new Test();
        t.start();
    }
}
```

![alt text](image-8.png)

## sleep method cases

**Case 1 : When multiple thread perfrom sleep method**

```java

class Test extends Thread{
    public void run(){
        for(int i = 1; i <= 5; i++){
            try{
                System.out.println(i + " : " + Thread.currentThread().getName());
                Thread.sleep(1000);
            }
            catch(Exception e){
                System.out.println(e);
            }
        }
    }
    public static void main(String args[]){
        Test t1 = new Test();
        t1.start();

        Test t2 = new Test();
        t2.start();
    }
}

//Output

/*
1 : Thread-1
1 : Thread-0
2 : Thread-1
2 : Thread-0
3 : Thread-1
3 : Thread-0
4 : Thread-1
4 : Thread-0
5 : Thread-1
5 : Thread-0
*/
```

In thi program both the thread get executed simultaneously and will take only 5 second.

**Case 2: When we use run() method instead of start() method**

```java

class Test extends Thread{
    public void run(){
        for(int i = 1; i <= 5; i++){
            try{
                System.out.println(i + " : " + Thread.currentThread().getName());
                Thread.sleep(1000);
            }
            catch(Exception e){
                System.out.println(e);
            }
        }
    }
    public static void main(String args[]){
        Test t1 = new Test();
        t1.run();

        Test t2 = new Test();
        t2.run();
    }
}

//Output

/*
1 : main
2 : main
3 : main
4 : main
5 : main
1 : main
2 : main
3 : main
4 : main
5 : main
*/

```

In this program both the object will execute the method separately and it will take 10 second to execute completly.

## yield() method.

- It is a method which stops the current executing thread and give a chance to other thread for execution.
- Working :
  - In java 5 internally it used sleep method.
  - In java 6 Thread provides the hint to the thread scheduler that it need to stop, then it depends on thread scheduler to accept or ignore the hint
- Method : `java public static native void yield(); `

**Program**

```java
class Test extends Thread{
    public void run(){
        for(int i = 1; i <= 5; i++){
            System.out.println(Thread.currentThread().getName() +  " - " + i);
        }
    }
    public static void main(String args[]){
        Test t = new Test();
        t.start();
        Thread.yield();
        for(int i = 1; i <= 5; i ++){
            System.out.println("Main thread :  " + i);
        }
    }
}
```

## join() method

- If a thread wants to wait for another thread to complete its task then we should use join() method.

**Methods**

- public final void join() throws InterruptedException{ }
- public final synchronized void join(long ms){ }
- **Program 1**

```java
public class Test extends Thread{
    public void run(){
        try{
            for(int i = 1; i <= 5; i ++){
                System.out.println("Chil thread " + i);
                Thread.sleep(1000);
            }
        }
        catch(Exception e){
            System.out.println(e);
        }
    }
    public static void main(String args[]) throws InterruptedException{
        Test t = new Test();
        t.start();
        t.join();//It will wait for the child thread to get executed completely then main thread will run.
         try{
            for(int i = 1; i <= 5; i ++){
                System.out.println("Main thread " + i);
                Thread.sleep(1000);
            }
        }
        catch(Exception e){
            System.out.println(e);
        }
    }
}

```

**Program 2**

```java
public class Test extends Thread{
    static Thread mainthread;
    public void run(){
        try{
            mainthread.join();//It will wait for the mainthread to completly execute before it gets executed.
            for(int i = 1; i <= 5; i ++){
                System.out.println("Chil thread " + i);
                Thread.sleep(1000);
            }
        }
        catch(Exception e){
            System.out.println(e);
        }
    }
    public static void main(String args[]) throws InterruptedException{
        mainthread = Thread.currentThread();//created reference for the main thread
        Test t = new Test();
        t.start();
         try{
            for(int i = 1; i <= 5; i ++){
                System.out.println("Main thread " + i);
                Thread.sleep(1000);
            }
        }
        catch(Exception e){
            System.out.println(e);
        }
    }
}

```

**Program 3**

```java
class Medical extends Thread{
    public void run(){
        try{
            System.out.println("Medical starts");
            Thread.sleep(3000);
            System.out.println("Medical completed");
        }
        catch(Exception e){
            System.out.println(e);
        }
    }
}
class TestDrive extends Thread{
    public void run(){
         try{
            System.out.println("TestDrive starts");
            Thread.sleep(5000);
            System.out.println("TestDrive completed");
            }
        catch(Exception e){
            System.out.println(e);
            }
    }
}
class OfficerSign extends Thread{
    public void run(){
         try{
            System.out.println("Officer takes the file");
            Thread.sleep(5000);
            System.out.println("Officer work completed");
            }
        catch(Exception e){
            System.out.println(e);
            }
    }
}
public class LicenseDemo{
    public static void main(String args[]) throws InterruptedException{
        Medical medical = new Medical();
        medical.start();
        medical.join();
        TestDrive td = new TestDrive();
        td.start();
        td.join();
        Officersign os = new OfficerSign();
        os.start();
    }
}
```

## Difference between yield() , join() and sleep().

![alt text](image-9.png)

## interrupt() method

- It is used to interrupt an executing thread.
- interrupt() method will only work when the thread is in sleeping(sleep()) or waiting state(wait()).
- It will change the interrupt status to true.
- When we use interrupt() method it throws an exception i.e InterruptedException.
- If a thread is not in sleeping or waiting state then calling an interrupt method will perform normal behavior.

**Syntax**

public void interrupt(){}

**Program**

```java
class Test extends Thread{
    public void run(){
        try{
            for(int i = 1; i < 5; i ++){
                System.out.println(i);
                Thread.sleep(1000);//As soon it will find sleep method it will get interrupted. If there is no sleep() method then the program will run normally there will be no effect of interrupt method.
            }
        }
        catch(Exception e){
            System.out.println("Thread interrupted : " + e);
        }
    }
    public static void main(String args[]){
        Test t = new Test();
        t.start();
        t.interrupt();
    }
}
```

## interrupted() and isInterrupted() method.

- Both interrupted() and isInterrupted() method is used to check whether a thread is interrupted or not.

**Difference**

- 1 Status

  - interrupted() method clear the interrupted status from true to false if the thread is interrupted.
  - isInterrupted() method does not clear the interrupted status.

- 2 Result

  - interrupted() method will change the result if called twice.
  - isInterrupted() method will produce the same result if called twice.

- 3 Syntax
  - public static boolean interrupted() { }
  - public boolean isInterrupted() { }

**Program - interrupted()**

```java
class Test extends Thread{
    public void run(){
        System.out.println(Thread.interrupted());//As it will change the status from true to false after displaying it true, so the program will not get interrupted and will work normally.
        try{
            for(int i = 1; i <= 5; i ++){
                System.out.println(i);
                Thread.sleep(1000);
            }
        }
        catch(Exception e){
            System.out.println("Thread interrupted : " + e);
        }
    }
    public static void main(String args[]){
        Test t = new Test();
        t.start();
        t.interrupt();
    }
}
```

**Program - isInterrupted()**

```java
class Test extends Thread{
    public void run(){
        System.out.println(Thread.currentThread().isInterrupted());//The status will be remain true so the interrupt() method will work properly and when it encounter sleep method it will get interrupted.
        try{
            for(int i = 1; i <= 5; i ++){
                System.out.println(i);
                Thread.sleep(1000);
            }
        }
        catch(Exception e){
            System.out.println("Thread interrupted : " + e);
        }
    }
    public static void main(String args[]){
        Test t = new Test();
        t.start();
        t.interrupt();
    }
}
```

## Synchronization

```java
class BookTheaterSeat{
    int total_seats = 10;
    void bookSeat(int seats){
        if(total_seats >= seats){
            System.out.println(seats + " seats booked successfully");
            total_seats = total_seats - seats;
            System.out.println("Seats left: " + total_seats);
        }
        else{
            System.out.println("Seats cannot be booked");
            System.out.println("Seats left: " + total_seats);
        }
    }
}
public class MovieBookApp extends Thread{
    static BookTheaterSeat b;
    int seats;
    public void run(){
        b.bookSeat(seats);
    }
    public static void main(String args[]){
        b = new BookTheaterSeat();
        MovieBookApp ashish = new MovieBookApp();
        ashish.seats = 5;
        ashish.start();
        MovieBookApp amit = new MovieBookApp();
        amit.seats = 6;
        amit.start();

    }
}
//The output in this program is very inconsistent as both the thread running siultaneously the resource which the both thread are sharing are manipulating according to the thread without caring about the other thread.
//When multiple threads are using the same resource the data should be consistent.
```

**Synchronization Introduction**

It is the process by which we can control the accesibilty of the multiple threads to a particular shared resource.

**Problem which can occur without synchronization**

- Data inconsistancy.
- Thread interference.

**Advantages of synchronization**

- No data inconsistency problem
- No thread interference

**Disadvantages of synchronization**

- Increase the waiting period of the thread.
- Create performace problem.(To overcome synchronization disadvantages, java provide one package i.e java.util.concurrent).

![alt text](image-10.png)

## Synchronized method

```java
class BookTheaterSeat{
    int total_seats = 10;
   synchronized void bookSeat(int seats){//Synchronized method
        if(total_seats >= seats){
            System.out.println(seats + " seats booked successfully");
            total_seats = total_seats - seats;
            System.out.println("Seats left: " + total_seats);
        }
        else{
            System.out.println("Seats cannot be booked");
            System.out.println("Seats left: " + total_seats);
        }
    }
}
public class MovieBookApp extends Thread{
    static BookTheaterSeat b;
    int seats;
    public void run(){
        b.bookSeat(seats);
    }
    public static void main(String args[]){
        b = new BookTheaterSeat();
        MovieBookApp ashish = new MovieBookApp();
        ashish.seats = 5;
        ashish.start();
        MovieBookApp amit = new MovieBookApp();
        amit.seats 6;
        amit.start();

    }
}
```

- If you declare any method as synchronized, it is known as synchronized method.

- Synchronized method is used to lock an object for any shared resource.

- When a thread invokes a synchronized method, it automatically acquires the lock for that object and releases it when the thread completes its task.

## Synchronized block

Synchronized block can be used to perform synchronization on any specific resource of the method.

Suppose we have 50 lines of code in our method, but we want to synchronize only 5 lines, in such cases, we can use synchronized block.

If we put all the codes of the method in the synchronized block, it will work same as the synchronized method.

### Important points to remember

- Synchronized block is used to lock an object for any shared resource.
- Scope of synchronized block is smaller than the method.
- A Java synchronized block doesn't allow more than one JVM, to provide access control to a shared resource.
- The system performance may degrade because of the slower working of synchronized keyword.
- Java synchronized block is more efficient than Java synchronized method.

```java
class BookTheaterSeat{
    int total_seats = 10;
   void bookSeat(int seats){
    System.out.println("Hello " + Thread.currentThread().getName());
    System.out.println("Hello " + Thread.currentThread().getName());
    System.out.println("Hello " + Thread.currentThread().getName());
    System.out.println("Hello " + Thread.currentThread().getName());
    System.out.println("Hello " + Thread.currentThread().getName());
    synchronized(this){//Synchronized block so that the code outside the block can run independently without waiting for the synchronized code to get executed.
        if(total_seats >= seats){
            System.out.println(seats + " seats booked successfully");
            total_seats = total_seats - seats;
            System.out.println("Seats left: " + total_seats);
        }
        else{
            System.out.println("Seats cannot be booked");
            System.out.println("Seats left: " + total_seats);
        }
    }
    System.out.println("Hello " + Thread.currentThread().getName());
    System.out.println("Hello " + Thread.currentThread().getName());
    System.out.println("Hello " + Thread.currentThread().getName());
    System.out.println("Hello " + Thread.currentThread().getName());
    System.out.println("Hello " + Thread.currentThread().getName());
    }

}
public class MovieBookApp extends Thread{
    static BookTheaterSeat b;
    int seats;
    public void run(){
        b.bookSeat(seats);
    }
    public static void main(String args[]){
        b = new BookTheaterSeat();
        MovieBookApp ashish = new MovieBookApp();
        ashish.seats = 5;
        ashish.start();
        MovieBookApp amit = new MovieBookApp();
        amit.seats 6;
        amit.start();

    }
}
```

## static synchronization

```java
class BookTheaterSeat{
   static int total_seats = 20;
   synchronized static void bookSeat(int seats){//If you make any static method as synchronized, the lock will be on the class not on object.
        if(total_seats >= seats){
            System.out.println(seats + " seats booked successfully");
            total_seats = total_seats - seats;
            System.out.println("Seats left: " + total_seats);
        }
        else{
            System.out.println("Seats cannot be booked");
            System.out.println("Seats left: " + total_seats);
        }
    }
}

class MyThread1 extends Thread{
    BookTheaterSeat b;
    int seats;
    MyThread1(BookTheaterSeat b, int seats){
        this.b = b;
        this.seats = seats;
    }
    public void run(){
        b.bookSeat(seats);
    }
}

class MyThread2 extends Thread{
    BookTheaterSeat b;
    int seats;
    MyThread2(BookTheaterSeat b, int seats){
        this.b = b;
        this.seats = seats;
    }
    public void run(){
        b.bookSeat(seats);
    }
}

public class MovieBookApp{
    public static void main(String args[]){
        BookTheaterSeat b1 = new BookTheaterSeat();
        MyThread1 t1 = new MyThread1(b1, 7);
        t1.start();
        MyThread2 t2 = new MyThread2(b1, 6);
        t2.start();


        BookTheaterSeat b2 = new BookTheaterSeat();
        MyThread1 t3 = new MyThread1(b2, 5);
        t3.start();
        MyThread2 t4 = new MyThread2(b2, 9);
        t4.start();
    }
}
```


**Problem without Static synchronization**

Suppose there are two objects of a shared class (e.g. BookTheaterSeat) named b1 and b2. In case of synchronized method and synchronized block there cannot be interference between t1 and t2 or t3 and t4 because t1 and t2 both refers to a common object that have a single lock. But there can be interference between t1 and t3 or t2 and t4 because t1 acquires another lock and t3 acquires another lock. We don't want interference between t1 and t3 or t2 and t4. Static synchronization solves this problem.

**Static Synchronization**

If you make any static method as synchronized, the lock will be on the class not on object.

## Inter-thread communication

Inter thread communication is a mechanism in which thread releases the lock and enter into paused state and another thread acquires the lock and continue to get executed.

It is implemented by following objects of method class.

**1. wait()** - If any thread calls the wait() method, it causes the current thread to release the lock and wait until another thread invokes the notify() or notifyAll() method for this object or a specified amount of time has elapsed.

**Syntax** 
- ```java public void final wait() throws InterruptedException``` (wait until object is notified)

- ```java public final void wait(long timeout) throws InterruptedException``` (waits for the specified amount of time)

**2. notify()** - This method is used to wake up a single thread and releases the object lock.

**Syntax**

- ```java public final void notify() ```

**3. notifyAll()** - This method is used to wake up all threads which are in waiting state.

**Syntax**

- ```java public final void notifyAll()```

**NOTE** - To call wait(), notify(), or notifyAll() method on any object, thread should own the lock of that object i.e thread should be in synchronized area.


```java

class TotalEarnings extends Thread{
    int total=0;
    public void run(){
        synchronized(this){
            for(int i = 1; i <= 10; i++){
            total = total + 100;
          }
          this.notify();//As soon as this method called by the thread 0 main thread will get executed.
        }
    }
}
public class MovieBookApp{
    public static void main(String args[]) throws InterruptedException{
        TotalEarnings t = new TotalEarnings();
        t.start();
        // System.out.println("Total earnings : "+t.total);//This will print the output 0 as main thread will complete its execution before thread 0 so to fix this we have to use wait() and notify() method
        synchronized(t){
            t.wait();//Main thread will wait till the jvm dont run notify() method.It will release the lock and will wait till another thread invokes the notify() method.
            System.out.println("Total earnings : "+t.total);
        }
    
    }
}

