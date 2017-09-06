# Notes for OS, Week 3, September 6th

## Announcements and Recap
    - vSphere Client will be installed in ENGR138
    - Processes
        - Dedicated memory space
        - Creation/switch is expensive
    - Threads
        - Threads from the same process share memory space
        - Creation/switch is fast
        - Pthread interface

## Implementing Threads in User-Space
    - User-level threads: the kernel knows nothing about them
        - OS Thinks there's only a single-threaded process
        - Doesn't involve multiplexing between processes so no kernel provilege required
        - Just save/restore registers
    - See Diagram on Slides

## User-level Threads - Discussion
    - Advantages
        - No OS thread-support needed
        - Lightweight: thread switching vs. process switching
            - Local procedure vs. system call (trap to kernel)
        - Each has its own customised scheduling algorithm
            - thread_yield()
    - Disadvantages
        - How do you block system calls? Called by a thread?
            - Goal: to allow each thread to use blocking calls, but to prevent one blocked thread from
                affecting the others.
            - How to change the blocking system calls to non-blocking?
        - Jacket/wrapper: library code to help check in advance if a call will block
        - How to deal with page faults?
        - How to stop a thread from running forever? No clock interrupts in a single process.
            - Garbage Collector? GCs can handle this, as shown by Go.

## Implementing Threads in the Kernel
    - Kernel-level threads: When a thread blocks, kernel re-schedules another thread
        - Threads known to OS
            - Scheduled by the scheduler
        - Slow
            - Trap into the kernel mode
        - Expensive to create and switch
            - Less expensive if in the same process
            - Registers, PC, stack pointer need to be created/changed
            - Not the memory management info
                Any Problems???
    - Write a program that forks from a multithreaded process
    - Please see diagram on slides

## Threading Models
    - N:1 (User-level threading)
        - N user threads that look like 1 to the OS kernel
    - 1:1 (Kernel-level threading)
        - Each user-thread is paired with a kernel-thread (aka native thread)
    - M:N (Hybrid Threading)
        - Solaris

## Threads in Linux
    - Thread control block (TCB)
        - The thread_struct structure
        - Includes registers and process-specific context
    - Linux treats threads like processes
        - 

## Summary
    - Processes vs. Threads
    - Why threads?
        - Concurrency + lightweight
    - Threading models
        - N:1, 1:1, M:N
    - Additional pactice
        - Find out what threading model does Java belong to
        - Write (download) a simple multithreaded java program
        - When it is running, issue ps -eLf | grep PROGRAMNAME

## What is CPU scheduling?
    - Five State Process Model
        - See slides, dawg
    - CPU scheduling
        - Selects from among the processes/threads that 
          are ready to execute, and allocates the CPU to it.

## Why CPU scheduling?
    - In support of multiprogramming
        - Uniprocessor systems
            - Time-sharing processor
        - Multiprocessor systems
            - Efficiently distributing tasks
        - Real-time systems
            - Reliably guaranteeing deadlines
    - It is (maybe) the most important part of an OS
        - Why do some OSs seem to be faster than others?
        - Why do I not see performance improvement when upgrading to a 16-core computer?

## CPU Scheduling
    - What does CPU schedule?
        - Processes or threads
    - Process context
        - Minimal set of state info that must be stored to allow a
            process to be stopped and restarted later.
        - Information stored in the CPU
            - Contents of registers
            - Program counter
        - Information stored in RAM

## CPU Scheduling
    - CPU scheduling may take place at
        - Non-preemptive
            - I/O Completion
            - Termination
        - Preemptive
            - Clock interrupts
            - I/O Interrupts
    - Non-preemptive
        - Scheduling only when the current process terminates or gives up control
    - Preemptive
        - Processes can be forced to give up control

## Scheduling Goals
    - All Systems aim for
        - Fairness - giving each process a fair share of the CPU
        - Policy enforcement - seeing that stated policy is carried out
        - Balance - keeping all parts of the system busy
    - Batch
        - Throughput - maximise jobs per hour
        - Turnaround time - minimise time between submission and termination
        - CPU utilisation - Keep the CPU busy at all times
    - Interactive
        - Response time - respond to requests quickly
        - Proportionality - Meet users' expectations
    - Real-time systems
        - Meeting deadlines - avoid losing data
        - Predictability - avoid quality degradation in multimedia systems

## Scheduling Goals: A Different Point of View
    - User Oriented -> minimise
        - Response time (wait time): the time that the first response is received (interactivity)
        - Turnaround time: the time that the task finishes
        - (Un)Predictability: variations in different runs
    - System oriented -> maximise
        - Throughput: Number of tasks that finish per CPU cycle
        - Utilisation: the percentage of time that the CPU is busy
        - Fairness: avoid starvation

## Process Behaviors
    - See Slides, Dawg

## Scheduling Polices
    - Batch Systems
        - First-Come, First-Serve
        - Shortest Job First
    - Interactive Systems
        - Round-Robin
        - Priority Q

## More on Scheduling Policy
    - Determine the next ready task to run
        - How we design pick_next_task()


## First-Come, First-Serve (FCFS)
    - See the slides

## Shortest Job First (SJF)
    - See the slides
    