# Notes for Operating Systems, 9/27/2017

## Readers and Writers Problem
    - Basically discussing parallel reading/writing is bad unless you're marking changes.
    - See the code on Slide 40

## Summary
    - Monitors, message passing, barriers
    - Classical IPC problems
    - Additional Practice
        - Linux Docs
        - Linux Docs
        - Spinlock vs. Mutex

## POSIX Threads Programming

## The Thread Model
    - Process: for resource grouping and execution
    - Thread: a finer-granularity entity for execution and parallelism 
        - Lightweight processes, multi-threading
    - Diagram on Slide 3
    - Because Threads within the same process share resources
        - Changes made by one thread to shared system resources (closing a file) will be seen by all other threads
        - Two pointers having the same value point to the same data
        - Reading and writing to the same memory location is possible, and therefore requires explicit synchronisation by the programmer. 

## Pthreads Overview
    - What are Pthreads?
        - An IEEE standardardised thread programming interface (IEEE POSIX 1003.1c)
        - POSIX (Portable Operating System Interface) threads
        - Defined as a set of C language programming types and procedure calls, implemented with a pthread.h header
    - SWEs view threads as a procedure that run independently from the main program

## Designing Threaded Programs
    - A program must be able to be organised into discrete, independent tasks which can execute concurrently.
        - E.G. Routine 1 and Routine2 can be interchanged, interleaved, and/or overlapped in real time
        - Thread-safeness: Ability to execute threads simultaneously without creating race conditions

## The Pthreads API
    - The API is defined in the ANSI/IEEE POSIX 1003.1 - 1995
        - Naming conventions: all identifiers in the library begin with pthread_
        - Three major classes of subroutines:
            - Thread management, mutexes, conditional variables
    