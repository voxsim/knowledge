## Concurrency
Concurrency is when two or more tasks can start, run, and complete in overlapping time periods. It doesn't necessarily mean they'll ever both be running at the same instant. Eg. multitasking on a single-core machine.

It enables parallelism, but it is different. If you have only one processor, you program can still be concurrent but it cannot be parallel.

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
