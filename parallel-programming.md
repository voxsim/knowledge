## Concurrency
Concurrency is when two or more tasks can start, run, and complete in overlapping time periods. It doesn't necessarily mean they'll ever both be running at the same instant. Eg. multitasking on a single-core machine.

## Parallelism
Parallelism is when tasks literally run at the same time, eg. on a multicore processor.

## Threading
Pro
- No rethinking is necessary
- Blocking program are ok
- The program lives until one thread is live

Cons
- Stack memory per thread
- If two threads use the same memory, a race can occur..
- Overhead
- Deadlock
- Thinking about realability is difficult
- System/Application confusion

### Mutual exclusion
- Semaphore
- Monitor
- Rendezvous
- Synchronization

This is used to be operating system stuff. It is leaked in the application world because of networking and multi-core problem.
The mutual exclusion is employed when two threads when two threads interact in the same critical section.
In some cases of mutual exclusion, a deadlock can occur when threads are waiting each other.
Managing sequential logic is hard, managing temporal logic is really really hard.

## Event Loop
Pro:
- Completely free of races and deadlocks
- Only one stack
- Very low overhead
- Resilient. If a turn fails, it can go on.

Cons:
- Program must never block
- Programs are inside out
- Turns must finish quickly (not good for long running tasks)

### Solutions for long running tasks
- Eteration: Break the tasks into multiple turns
- Move the task into a separate process (worker)

More Info:
- [ ] Computer Science 162 - Operating Systems (25 videos):
    - for processes and threads see videos 1-11
    - [Operating Systems and System Programming (video)](https://www.youtube.com/playlist?list=PL-XXv-cvA_iBDyz-ba4yDskqMDY6A1w_c)
- [What Is The Difference Between A Process And A Thread?](https://www.quora.com/What-is-the-difference-between-a-process-and-a-thread)
- Covers:
    - Processes, Threads, Concurrency issues
        - difference between processes and threads
        - processes
        - threads
        - locks
        - mutexes
        - semaphores
        - monitors
        - how they work
        - deadlock
        - livelock
    - CPU activity, interrupts, context switching
    - Modern concurrency constructs with multicore processors
    - [Paging, segmentation and virtual memory (video)](https://www.youtube.com/watch?v=LKe7xK0bF7o&list=PLCiOXwirraUCBE9i_ukL8_Kfg6XNv7Se8&index=2)
    - [Interrupts (video)](https://www.youtube.com/watch?v=uFKi2-J-6II&list=PLCiOXwirraUCBE9i_ukL8_Kfg6XNv7Se8&index=3)
    - [Scheduling (video)](https://www.youtube.com/watch?v=-Gu5mYdKbu4&index=4&list=PLCiOXwirraUCBE9i_ukL8_Kfg6XNv7Se8)
    - Process resource needs (memory: code, static storage, stack, heap, and also file descriptors, i/o)
    - Thread resource needs (shares above (minus stack) with other threads in the same process but each has its own pc, stack counter, registers, and stack)
    - Forking is really copy on write (read-only) until the new process writes to memory, then it does a full copy.
    - Context switching
        - How context switching is initiated by the operating system and underlying hardware
- [ ] [threads in C++ (series - 10 videos)](https://www.youtube.com/playlist?list=PL5jc9xFGsL8E12so1wlMS0r0hTQoJL74M)
- [ ] concurrency in Python (videos):
    - [ ] [Short series on threads](https://www.youtube.com/playlist?list=PL1H1sBF1VAKVMONJWJkmUh6_p8g4F2oy1)
    - [ ] [Python Threads](https://www.youtube.com/watch?v=Bs7vPNbB9JM)
    - [ ] [Understanding the Python GIL (2010)](https://www.youtube.com/watch?v=Obt-vMVdM8s)
        - [reference](http://www.dabeaz.com/GIL)
    - [ ] [David Beazley - Python Concurrency From the Ground Up: LIVE! - PyCon 2015](https://www.youtube.com/watch?v=MCs5OvhV9S4)
    - [ ] [Keynote David Beazley - Topics of Interest (Python Asyncio)](https://www.youtube.com/watch?v=ZzfHjytDceU)
    - [ ] [Mutex in Python](https://www.youtube.com/watch?v=0zaPs8OtyKY)

- https://www.quora.com/What-is-the-difference-between-a-process-and-a-thread
