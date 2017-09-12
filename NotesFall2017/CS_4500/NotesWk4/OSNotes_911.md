# OS Notes for 9/11/2017

## Announcements
    - No office hours: Thu 1-2PM
        - On Friday instead
    - Common Mistakes
        - /my_source/Makefile
            - obj-y := xxx.o yyy.o zzz.o
            - Should be +=, \, or just spaces.
        - KERN_EMERG
            - link
    - TA's Email
        - Omitted for privacy concerns

## FCFS
    - See slides

## SJF (Shortest Job First)
    - See slides

## Round Robin (RR)
    - See slides
    - Response time is super low
    - Turnaround is much higher (highest we've seen, I think)

## Priority Scheduling (PS)
    - See Slides

## Put It Together
    - FCFS - 15.25/8.75
    - SJF-Preemp - 13/4.25
    - RR(q=5) - 17.5/5.5
    - Priority Scheduling - NA/NA

      Methodology - Throughput - Response Time - Starvation

    - FCFS          Depends      Depends         No
    - SJFPreemp     High         Good            Yes
    - RR            Can be low   Good            No
    - PS            Can be high  Can be good     Can remove

## Multilevel Feedback Queue
    - Windows XP, MacOS X, Linux 2.6.22 and before.
    - High Priority/Short Task
    - Low Priority/Long Task
    - See Slides

## Real-time Scheduling
    - Schedulable real-time system
    - Given
        - m periodic events
        - Event i occurs with period Psubi seconds and requires Csubi seconds
    - Then the load can only be handled (schedulable) if:
        - M A T H
    - Example: a soft real-time system with three periodic events, with periods of 100, 200, and 500 ms, respectively. If these events require 50, 30, and 100 ms of CPU time per event, respectively, the system is schedulable.
        - Process/context switching is often an issue though.
        - Given the example, what would be the maximum CPU burst for a 4th job with a period of 500ms?

## Multiprocessor -> many core
    - See slide 20

## Close look at State of the Art
    - See Slide 21
