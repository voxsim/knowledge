# Processes and Multithreading

Processes are the abstraction of running programs: A binary image, virtualized memory, various kernel resources, an associated security context, and so on. Threads are the unit of execution in a process: A virtualized processor, a stack, and program state.

Put another way, processes are running binaries and threads are the smallest unit of execution schedulable by an operating system's process scheduler.

A process contains one or more threads. In single-threaded processes, the process contains one thread. You can say the thread is the process—there is one thing going on. In multithreaded processes, the process contains more than one thread—there's more than one thing going on.

The two primary virtualized abstractions in modern operating systems are virtualized memory and a virtualized processor. Both afford the illusion to running processes that they alone consume the machine's resources. Virtualized memory gives processes a unique view of memory that seamlessly maps back to physical RAM or on-disk storage (swap space). A virtualized processor lets processes act as if they alone run on a processor, when in fact multiple processes are multitasking across multiple processors.

Virtualized memory is associated with the process and not the thread. Thus, threads share one memory address space. Conversely, a distinct virtualized processor is associated with each thread. Each thread is an independent schedulable entity.

What's the point? We obviously need processes. But why introduce the separate concept of a thread and allow multithreaded processes? There are four primary benefits to multithreading:

* Programming abstraction. Dividing up work and assigning each division to a unit of execution (a thread) is a natural approach to many problems. Programming patterns that utilize this approach include the reactor, thread-per-connection, and thread pool patterns. Some, however, view threads as an anti-pattern. The inimitable Alan Cox summed this up well with the quote, "threads are for people who can't program state machines."
* Parallelism. In machines with multiple processors, threads provide an efficient way to achieve true parallelism. As each thread receives its own virtualized processor and is an independently-schedulable entity, multiple threads may run on multiple processors at the same time, improving a system's throughput. To the extent that threads are used to achieve parallelism—that is, there are no more threads than processors—the "threads are for people who can't program state machines" quote does not apply.
* Blocking I/O. Without threads, blocking I/O halts the whole process. This can be detrimental to both throughput and latency. In a multithreaded process, individual threads may block, waiting on I/O, while other threads make forward progress. Asynchronous & non-blocking I/O are alternative solutions to threads for this issue.
* Memory savings. Threads provide an efficient way to share memory yet utilize multiple units of execution. In this manner they are an alternative to multiple processes.

The cost of these benefits of threading are increased complexity in the form of needing to manage concurrency through mechanisms such as mutexes and condition variables. Given the growing trend toward processors sporting multiple cores and systems sporting multiple processors, threading is only going to become a more important tool in system programming.
