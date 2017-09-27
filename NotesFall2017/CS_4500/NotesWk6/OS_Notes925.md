# OS Notes for 9/25/17

## Busy Waiting: Pros and Cons
    - Cons
        - Wastes CPU Cycls
        - For single-core system, user-level threads
            - T1 waiting for T2 to change lock to 0
            - T1 never gets to run when T2 is running
    - Pros
        - Avoids expensive context switch when critical region is very short
            - Sleep/wakeup (an alternative to busy waiting) requires context switch
                - Time putting a thread to sleep/waking it up might exceed their time limit

## Semaphores and P/V Operations
    - Semaphores: a variable to indicate the # of pending wakeups (Djikstra)
    - Down operation (P; request): Lock/Sleep
        - Checks if a semaphore is > 0:
            If so, it decrements the value and continues
            Otherwise (==0) the process is put to sleep without completing the down for the moment
    - Up operation (V; release): unlock/wakeup
        - Increments the value of the semaphore
            If one or more processes are sleeping on the semaphore, one of them is chosen by the system (randomly) and allowed to complete its down (semaphore will still be 0)

## Mutexes
    - A variable that can be in one of two states: unlocked or locked
    - A simplified version of the semaphores [0, 1]

## Mutexes - User-space Multi-threading
    - What is a key difference between mutex_lock and enter_region in multi-threading and multi-processing?
        - For user-space multi-threading, a thread 

## When to use Busy-waiting/Sleep-wakeup
    - On a single-core system
        - Using busy-waiting makes 0 sense
            - No other thread can run, lock won't be unlocked
        - Use sleep-wakeup instead
    - On a multi-core system, with locks held for very short periods
        - Time for putting threads to sleep/waking up might decrease runtime performance
        - Use busy-waiting instead
    - In practice: # of cores and architecture unknown
        - H y b r i d     a p p r o a c h

## Monitors
    - Monitor: A higher-level synchorinzation primitive
        - Only one process can be active in a monitor at any instant, with compiler's help; thus, how about putting all the critical regions into monitor procedures for mutual exclusion?
    - Diagram on Slide 27

## All previous methods
    - Work on a single computer
        - Assuming data can be shared in some way
    - Data exchange between machines?
        - Message passing
            - Inter-process communication using two primitives, send/receive
            - Send (destination, &message);
            - Receive(source, &message);
            - Syscalls rather than language constructes

## Barriers
    - Use of a barrier (for programs operating in phases, neither enters the next phase until all are finished with the current phase) for groups of processes to do synchronisation
        - Processes approaching a barrier
        - All processes but one are blocked
        - Last process arrives, all are let through

## Class IPC Problems: Dining Philosophers
    - Philosophers eat/think
    - Eating needs two forks
    - Pick one fork at a time
    - How to prevent deadlock and starvation
        - Deadlock: both are blocked on some resource
        - Starvation: Both are waiting, but no progress is made
        