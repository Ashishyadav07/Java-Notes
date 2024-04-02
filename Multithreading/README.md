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
