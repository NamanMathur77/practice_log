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


### What is multithreading in C#?
Multithreading is the process of running multiple threads concurrently within a single process to improve performance and responsiveness.

### What is a threadpool in C#?
A threadpool is a collection of reusable threads managed by .Net runtime, used for short lived background tasks.

### How do you stop a thread in C#?
Stopping a thread is done using flags or CancellationToken. Should not be done using Thread.Abort() as it is unsafe.
```C#
using System.Threading;
using System.Threading.Tasks;

class Program {
static void Main() {
CancellationTokenSource cts = new CancellationTokenSource();
Task.Run(() => {
while (!cts.Token.IsCancellationRequested) {
Console.WriteLine("Running...");
Thread.Sleep(500);
}
});

Thread.Sleep(2000);
cts.Cancel(); // Gracefully stop the task
}
}
```

### What are race conditions, and how to prevent them?
A race condition occurs when two or more threads access shared data at the same time, and final result depends on the timing of how those threads execute.

```C#
using System;
using System.Threading;

class Program
{
    static int counter = 0;

    static void Main()
    {
        Thread t1 = new Thread(Increment);
        Thread t2 = new Thread(Increment);

        t1.Start();
        t2.Start();

        t1.Join();
        t2.Join();

        Console.WriteLine($"Final Counter: {counter}");
    }

    static void Increment()
    {
        for (int i = 0; i < 100000; i++)
        {
            counter++;
        }
    }
}
```

Here the output in ideal condition is 200000 but sometimes when two thread are running concurrently one thread might increase the value while the other one read the previous value so both are increasing counter to same value or might be that the counter is increased more then 2 time in a single run so value can be 178889 ... 

To prevent this we may use
1. Lock
```C#
private static object _lock = new object();
private static int counter = 0;

static void Increment()
{
    for (int i = 0; i < 100000; i++)
    {
        lock (_lock)
        {
            counter++;
        }
    }
}
```

through this one thread at a time can enter the lock block while others wait until the lock is released 

2. Monitor
```C#
using System;
using System.Threading;

class Program
{
    // Shared variable between threads
    static int counter = 0;

    // Lock object to synchronize access
    private static readonly object _lock = new object();

    static void Main()
    {
        Thread t1 = new Thread(Increment);
        Thread t2 = new Thread(Increment);

        t1.Start();
        t2.Start();

        t1.Join();
        t2.Join();

        Console.WriteLine($"Final Counter: {counter}");
    }

    static void Increment()
    {
        for (int i = 0; i < 100000; i++)
        {
            // Acquire lock manually
            Monitor.Enter(_lock);
            try
            {
                counter++;
            }
            finally
            {
                // Always release the lock, even if an exception occurs
                Monitor.Exit(_lock);
            }
        }
    }
}
```

### What is asynchronous programming?
Asynchronous programming is a way to execute code without blocking the main thread allowing other tasks to execute. That is allows other tasks to execute without waiting for long running tasks.

#### Asynchronous code
```C#
Console.WriteLine("Start");
var data = await File.ReadAllTextAsync("bigfile.txt"); // Non-blocking
Console.WriteLine("File read complete");
Console.WriteLine("End");
```

C# handles the asynchronous programming through async and await.
```C#
public async Task FetchDataAsync()
{
    Console.WriteLine("Fetching data...");
    
    // Simulate long-running task (e.g., web request)
    await Task.Delay(3000); // Wait for 3 seconds asynchronously
    
    Console.WriteLine("Data fetched!");
}
```

1. async tells the compiler that this method will contain asynchronous operations.
2. await pauses the method until the awaited task completes.
3. The thread is freed during the wait time and can handle other work.


