# OS Notes for 9/13/2017

## Recap
    - Basic scheduling processors on uniprocessors
        - FCFS                          ---\
        - Shortest Job First            ----\
        - Round Robin                   ------> Time-sharing: Which thread should run next
        - Priority Scheduling           ----/
        - Multilevel feedback queue     ---/

## Multoprocessor Scheduling
    - Two-dimension schedling
        - Time-sharing on each processor                -\
        - Load-balancing among multiple processors      --> Which thread to run and where?
    - Several issues
        - Why load balancing?                       --> Take advantage of parallelism
        - Simple time-sharing?                      --> No, because you need to consider a group now
        - Are all processors/cores equal            --> No, cache affinity/cache hotness, memory locality makes them different

## Multiprocessor Hardware
    - UMA
        - Uniform Memory Access
    - FSB
    - DRAM Controller
    - Memory

## Ready Queue Implementation
    - A single system-wide ready queue
    - Ready Queue -> pick_next_task  --> Processor
                                    \
                                     --> Processor
    - Pros:
        - Easy to Implement
        - Perfect Load Balanacing
    - Cons
        - Scaling Issues due to centralised synchronisation
        - High overhead and low efficiency
            - Hard to maintain cache hotness

## Cont'd
    - 1:1 queue to processor.
    - Pros
        - Scalable to many CPUs
        - Easy to maintain cache hotness
    - Cons
        - More complex
        - Not perfect load balancing -> not always balanced

## Push Model vs. Pull Model
    - Push Model
        - Kernel thread periodically checks load imbalance and moves threads
    - Pull Model
        - Go model.
        - Steals from non-empty queues
    - See Slides

## Scheduling Parallel Programs
    - A parallel job
        - A collection of processes/threads that cooperate to solve the same problem
        - Scheduling matters in overall job completion time
    - Why scheduling matters.
        - Synchronisation on shared data (mutex)
        - Causality between threads (producer <-> consumer)
        - Synchronisation on execution phases (barrier)

## SPAAAAAAAACE Sharing
    - Divide Processors into Groups
        - Dedicate each group to a parallel job
        - No preemption before job completion
    - 8CPU/6CPU/4CPU/12CPU partition
    - 2 unassigned. 
    - Pros
        - Highly efficient for processes/threads, low overhead (no context switch)
        - Strong affinity
    - Cons
        - Highly inefficient for CPUs, cycle waste
        - I n f l e x i b l e

## Time Sharing: Gang or Co-Scheduling
    - Each processor runs threads from multiple jobs
        - Groups of related threads are scheduled together as a unit: a gang
        - All CPUs perform context switches together

## Summary
    - Multiprocessor hardware
    - Two implementations of the ready queue
        - A single queue vs. multiple queues
        - Push model vs. Pull model
    - Parallel program scheduling
        - Space sharing vs. Time Sharing
    - Resources hype.

## Inter-Process Communication (IPC)
    - Three fundamental issues
        - How does one process pass information to another
        - How to make sure two or more processes do not get in the way of each other during critical activities
        - How to maintain proper sequenicng when dependencies present
    
        - How about inter-thread communication?

## Race Conditions
    - Race conditions: when two or more processes/threads are reading or writing some shared data and the final     results depend on who runs precisely when. 
        - Interrupts, interleaved operations/execution

## Mutual Exclusion and Critial Regions
    - Mutual Exclusion: makes sure if one process is using a shared variable or file, the same processes will be    excluded from doing the same thing.
    - Critical Regions: the part of the program where the shared memory is accessed.
    - Four conditions to provide mutual exclusion
        - No two processes simultaneously in critical region
        - No assumptions made about speeds or number of CPUs
        - No processes running outside its critical region may block another process
        - No process must wait forever to enter its critical region

## Mutual Exclusion with Busy Waiting
    - Disabling Interrupts:
        - OS technique, not user
        - Multi-CPU?
    - Lock variables:
        - Test-set is a two-step process, not atomic
    - Busy waiting:
        - Continuously testing a variable until some real value appears (spin lock bby)

## Busy Waiting: Strict Alternation
    - See Slide 9

## 