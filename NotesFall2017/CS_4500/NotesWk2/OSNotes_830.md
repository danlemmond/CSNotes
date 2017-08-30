# OS Notes for 8/30

## init and systemd
    - New systems run systemd due to its parallel nature
    - Older systems run init, which can only initialise one process at a time
        - I almost typed programmed, close

## Process Life Cycle
    - See diagram in slides.
    - New, Ready, Running, Terminated, (Blocked)
        - Ready:
            - Willing to run, wait for the CPU
        - Blocked:
            - Unable to run, wait for an event
        - LOCKS AND SEMAPHORES, IS THAT YOU.
        - While waiting for locks or semaphores, is that a block or a ready?
    - Scheduler:
        - Needs to schedule this process in order to allow the process to run
    - Running -> Ready
        - Interrupted by timer or preemption
        - Preemption:
            - Runs a PriorityQueue/Priority system in order to move from running -> ready in order to manage more important processes.
            - Can I edit or change the priority of a process?

## Implementation of Processes
    - Process Table
        - One entry per process
        - Each entry is called a process control block (PCB)
    - Process Control Block (PCB)
        - OS/Kernel data structure containing data associated with processes

## Linux Processes
    - Process Table: implemented as a linked list/hashtable
        - Each element: a process descriptor of type struct task_struct
        - Dynamically allocated for each process
        - Process Descriptor
            - Contains all info about a specific process
    - See diagram in slides
    - PCB/Process Descriptor
        - See Diagram

## Linux Process Descriptor
    - State
        - TASK_RUNNING
        - TASK_INTERRUPTABLE
        - EXIT_ZOMBIE
    - Identifiers
    - Scheduling info
    - File system
    - Virtual memory
    - Others
    - SEE DIAGRAM

    - Identifiers
        - PID
            - PID of the process/thread
        - TGID
            - PID of the thread group leader
        - PGRDP
            - PID of the group leader
    - How to get the pointer to a specific process?
        - Use the CURRENT macro
        - Use the INIT_TASK macro
        - Use FIND_TASK_BY_VPID(PID_T PID)

    task_struct &task;
    for (task = current;) {
        task != &init_task;
        task = task.parent_id;
    }

    - Files
        - fs_struct
            - File system information: root directory, current directory
        - files_struct
            - Information on opened files
    
## Summary
    - What is a process?
        - An instantiation of a program
    - Program life cycle:
        - Ready, running, blocked, new, terminated
    - Process implementation
        - Process table, PCB
    - Additional Practice
        - Download linux kernel source to the VM, find the following fields in structure task_struct, in LINUX_SRC_FOLDER/include/linux/sched.h

## Thread and Multithreading
    - Process
        - Resource grouping and execution
            - Stack/Heap/Data/Text
    - Thread
        - Process is going to cook a feast
            - Feast requires multiple different tasks - but they all want to cook a feast
            - Must have recipe == instructions
        - Each thread does something
        - They share the same data but look at different parts
        - They have private state but can communicate easily
        - They must coordinate!
        - CON CURR EN CY

## An Illustration from the OS point of view
    - Yo Dawg, look at the diagram
    - Code / Data / Files are shared
    - Registers / Stack are kept separate to run their own processes

## Threads
    - Express concurrency
        - There are other ways to explore concurrency (e.g., non-blocking I/O), but they are difficult to program
    - Efficient communication
        - Communication can be carried out via shared data objects within the shared address space
        - Inter-process communication (IPC) usually requires other OS services: file system, network system
    - Efficient creation
        - Only create the thread context

## Thread and Multithreading
    - Thread
        - A finer-grained entity for execution and parallelism
        - Lightweight process
        - A program in execution without dedicated address space
    - Multithreading
        - Multiple threads in parallelism

##Threads vs. Processes: A closer look
    - Threads
        - No data segment or heap
        - Multiple can coexist in a process
        - Share code, data, heap, and I/O
        - Have own stack and registers
        - Inexpensive to create
        - Inexpensive context switch
        - Efficient communication
    - Processes
        - Have data/code/heap

## Thread Usage 1
    - Why not multiple processes?
        - Context switch = expensive
        - Hard to create multiple processes
    - Race Condition?
    - Processes share data, no reason for multiple if you're running across multiple threads
    - http.ListenAndServer(Go) can be done concurrently with Coroutines/Green Threads
        - Threads vs. Green Threads, expense between the two?
            - Green Threads are way cheaper and user schedule - overhead is much smaller.
            - 

## Thread interfaces in UNIX: POSIX threads
    - UNIX Systems
        - IEEE Portable Operating System Interface (POSIX)
        - Implementations of threads that adhere to this standard are referred to as POSIX threads or Pthreads

## Pthread Function
    int pthread_create(pthread_t *thread, const pthread_attr_t *attr, void *(*start_routine) (void *t)) {
        *Thread*
    }

