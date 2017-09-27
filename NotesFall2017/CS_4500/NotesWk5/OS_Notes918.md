# OS Notes for 9/18/17

## Race Conditions
    - Race Conditions: when two or more processes/threads are reading or writing some shared data and the final results
        depend on who runs precisely when
        - Interrupts, interleaved operations/execution

## Mutual Exclusion
    - See the slides

## Busy Waiting: Strict Alternation
    - See Slide for implementations

## Busy Waiting: Peterson's Implemetation
    - See slide for (very detailed) implementation

## Busy Waiting: TSL (Test and Set Lock)
    - See Slides

## Sleep and Wakeup
    - Issue I with Peterson's and TSL: how to avoid CPU-costly busy waiting?
    - Issue II: Priority inversion problem
    - Some IPC primitives that block instead of wasting CPU time when they are not allowed to enter their critical regions
        - Sleep and Wakeup

## 