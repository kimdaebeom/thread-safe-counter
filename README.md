# thread-safe-counter

#### - Class of Professor JongChan Kim.

#### - Project : Thread-Safety by Semaphore

#### - OS version : Ubuntu Linux 18.04 

- file [tscounter.c] is original file by mutex method, file [semaphore_tscounter.c] is fixed file by semaphore method.
- using time command    *ex> time ./a.out 10000*
--------------------------------------------------------

## Compare Performance

### by Mutex
<img src="https://user-images.githubusercontent.com/68265609/121745519-5dae1500-cb3f-11eb-87d9-6f3ede92f05e.png" width="700" height="420">

### by Semaphore
<img src="https://user-images.githubusercontent.com/68265609/121745533-63a3f600-cb3f-11eb-8864-3aa3fc98d54b.png" width="700" height="420">

#### -The table below shows the time taken according to the given count. The time is in order [real / user / sys].

- **Real** is wall clock time - time from start to finish of the call.
- **User** is the amount of CPU time spent in user-mode code (outside the kernel) whitin the process.
- **Sys** is the amount of CPU time spent in the kernel within the process.

##### -**We just have to focus on real, which means real factor time.**

|**Method**|**count : 10000**|**count : 100000**|**count : 100000**|
|:------:|:------:|:------:|:------:|
|**MUTEX**|[**0.004** / 0.006 / 0.000]|[**0.029** / 0.025 / 0.029]|[**0.186** / 0.204 / 0.164]|
|**SEMAPHORE**|[**0.061** / 0.006 / 0.080]|[**0.443** / 0.059 / 0.571]|[**4.715** / 0.468 / 6.237]|

---------------------------------------------------------

## Analysis

In Operating System, there are a lot of processes which are ready to be executed at a particular instant of time.
One thing that should be kept is mind is that the resources are shared but it should not be used simultaneously by all processes.
This is called **Process Synchronization**.
In parallel computing, a **critical section** is a piece of code that accesses shared resources (data structures or devices) that should not be accessed by more than one thread simultaneously.

To apply process synchronization, 2 methods are used.
One is **MUTEX**, which has already implemented as a project example.
And the other is **Semaphore** that we need to implement.

Mutex or Mutual Exclusion Object is used to give access to a resource to only one process at a time.
It is a locking mechanism that allows only one thread to obtain mutex at the same time and enter the critical section.
And only one thread can turn off mutex when it exits the critical area.

However, Semaphore differs from mutex in that it is a signalling mechanism.
It calls the wait function can call the signal function, in that even threads that don't lock can unlock it by sending signal.
It uses 2 atomic operations for synchronization : wait and signal.
Calling wait reduces the semaphore's count by one, and locks are executed when the semaphore's count is less than or equal to zero.

These are the basic difference between mutex and semaphore above.

In this project's case, semaphore can assume the values 0 and 1 only. It is called 'Binary Semaphore'.
So it means we have to analyze about the difference between binary semaphore and mutex.

Let's take a look at the table above. 
Depending on the performance time, you can see that mutex takes much less time than semaphore.

In general, Semaphore is faster than mutex because any other thread or process can unlock binary semaphore.
In mutex, only thread which has acquired must release the lock. So it is slower.
And there are a number of instances for resources, semaphore is faster.
But if you have single instance for resource, it is better to use Mutex.

