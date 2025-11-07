## Thread

#### A thread is smallest unit of execution in a process.
#### A process can have multiple threads and each thread executing some part of your program concurrently.

## Creating Thread
```C#
using System;
using System.Threading;

class Program
{
    static void Main()
    {
        Thread t = new Thread(DoWork);
        t.Start();

        for(int i = 0; i < 5; i++){
            Console.WriteLine("Main thread running");
            Thread.Sleep(500);
        }
    }

    static void DoWork()
    {
        for(int i = 0; i < 5; i++){
            Console.WriteLine("Worker thread running");
            Thread.Sleep(500);
        }
    }
}
```
#### Output - 
Main thread running
Worker thread running
Main thread running
Worker thread running
Main thread running
Worker thread running
Main thread running
Worker thread running
Main thread running
Worker thread running


## Thread Methods

| Method	  | Description                          |
| ----------- | ------------------------------------ |
| Start()	  | Starts thread execution              |
| Sleep(ms)   |	Pauses thread for milliseconds       |
| Join()	  | Waits for a thread to finish         |
| IsAlive	  | Checks if thread is still running    |


### What are Process?

Process is something that operating system uses to execute a program by providing the resources required. Processes can be viewed in the task manager.


### What is the difference between Thread and Process?

A process is a collection of resources like virtual address space, code etc. A process can start multiple threads. Every process starts with a single thread. You can create multiple threads in the process and threads share resources allocated to the process.

### Why do we need multi threading in our project?

1. You can do multiple tasks simultaneously.
2. Threads are lightweight than processes as they down own resources they use the resources allocated to process.
3. Context switching takes less time in threads.


