# OS Notes for 8/28

## Interactions between OS and I/O Devices
    - The OS gives commands to the I/O devices
    - The I/O device notifies the OS when the I/O device has completed an operation or has encountered an error
    - Data is transferred between memory and an I/O device.

## How do I/O devices notify the OS?
    - Hardware device events
        - Hardware devices produce eveents at times and in patterns not known in advance
            - Keyboard Presses
            - Incoming network packets
            - Mouse movements, etc.
    - How to make information generate by these events available to running applications?
        - Three methods: polling, interrupt, DMA
    - Polling (busy waiting)
        - The I/O device puts information in a status register
        - The OS periodically checks the status register
        - Simple design: OS periodically checks device
            - How often is periodically? What is based on?
        - Disadvantages:
            - Most time device has no input data - waste CPU time
            - High latency - device input must wait for polling interval
    - Interrupt (yelling)
        - Whenever an I/O device needs attention from the processor, it interrupts the processor from what it is currently doing
            - HW signals the OS when events occur
            - OS switches away from running processes, handles the event
            - More responsive than polling, but complex implementation
        - An interruption of the normal sequence of the execution
        - Improves processing efficiency (in comparison to polling)
        - A suspension of a process caused by an event external to that process and performed in such a way that the process can be resumed.
        - Types:
            - I/O
            - Timer
    - DMA (Direct Memory Access)
        - Direct memory access: delegate I/O responsibility from CPU (more in Chapter 5)

## I/O Interrupt
    a.
        1. CPU writes cmds in to device registers
        2. The device signals interrupt controller
        3. Interrupt controller informs CPU
        4. CPU accepts the interrupt and triggers the service routine. 
    b. 
        1. Save current instruction info, switch to kernel mode
        2. Find interrupt handler (service routne) for device
        3. Interrupt handler finishes: return to user program
    - Please see attached diagram

## System Calls
    - From last class: transition between user/kernel mode
        - Interrupt - HW device requests OS service
            - Event Triggered
            - Asynchronous
        - Trap - user program requests OS services: system calls
            - A user program needs a system service (reading a file): execute a **trap** instruction to transfer control to OS
            - OS inspects parameters, carries out system call, returns control to the instruction following the syscall
            - Program triggered
            - Synchronous
        - Exception: error handling

## SysCalls
    - See diagram

## Process Management
    - Process: A fundamental OS concept
        - Memory address space
        - Some set of registers (program counter, stack pointer)
        - Protection domain
        - Resource allocation
    - OS responsibilites for process management:
        - Process creation and deletion
        - Process scheduling, suspension, and resumption
        - Inter-process communication and synchronisation
        - LOCKS AND SEMAPHORES? IS THAT YOU?

## Memory Management (Chapter 2)
    - Memory
        - A large array of addressable words and bytes
    - OS responsibilities for memory management
        - Allocate and de-allocate memory space
        - Keep memory space efficiently utilised
        - Keep track of which part of memory are used and by whom

## File and Storage Mangagement (Chapter 3)
    - A file is a collection of data (usually) stored on disk with a unique name
        - Programs
        - Data
        - Devices (UNIX & Linux)
    - OS responsibilites for file management
        - Organise directories and files
        - Map files onto disk
    - OS responsibilites for disk management
        - Disk space management
        - Disk scheduling

## Additional Readings and Practice
    - Section 1.6 and try the following Linux commands
        - who, uname, ls, cat, cp, rm, mv, cd, mkdir, touch, chmod
        - Use "man" to see the manual of above commands
    - Write a C program with an output to the screen
        - strace -o trace.txt ./YOUR_PROG
        - See the system calls triggered
        - >reading<
    - Check the EAS cloud tutorial on course website

## Summary
    - Computer hardware:
        - Time Sharing: CPU
        - Space Sharing: memory, disk
    - OS componenets
        - Process management
        - Memory management
        - File and storage management

# Lecture 3
    - Process == program?

## Process
    - Definition:
        - An instance of a program running on one computer
        - An abstraction that supports running programs
        - An *execution stream* in the context of a particular *process state*.
        - A *sequential* stream of execution in its *own memory space*.
    - Two parts of a process:
        - Sequential execution of instructions
        - Process state:
            - Registers: PC/SP
            - Memory: address space, code, data, stack, heap
            - I/O status: open files

## Conclusion: Program != Process
    - Program:
        - Static code + data
        - Process = dynamic instantiation of code + data + files ...
    - No 1:1 mapping
        - A program can invoke many processes
        - Many processes of the same program
    - How does this work with concurrency?
        - Is each green thread a process?
        - Can each green thread run multiple processes?

## Process Model
    - See Diagram, ya doofus
    - A. Multiprogramming of four programs
    - B. Conceptual model of 4 independent, sequential processes
        - Sequential process mode: hiding the effects of interrupts, and support blocking sys calls. 
    - C. Only one program active at any instant

## Process Creation
    - Principal events that cause process creation
        - System initialisation; foreground and background
        - Execution of a process creation syscall
        - User request to create a new process; interactive systems
        - Initiation of a batch job
    - Unix Example
        - **fork** system call creates an **exact copy** of calling process
            - Git????
        - Same memory image, environment settings, and opened files
        - After fork, caller is parent, newly created process is child
        - Is this why global vars are bad?
            - Stack overflows and exploitation of the data layer
            - If global vars are stored in data, easier to access
            - Local vars would be harder to access as part of the stack
        - Child process calls **execve** to change its memory image and run a new program

## After fork()
    - The child process returns executing at the exact same point after its parent called fork()
        - Fork returnrs twice: the new PID to the parent, and 0 to the child
            ```
            pid = fork();
            if (pid == 0){
                /* I am the child (0: invalid PID) */
            } else {
                /* I am the parent */
            }
            ```
        - All memory contents of parent/child are identical
        - Both have the same files open at the same position (point to the same object files)

## Process Termination
    - Conditions which terminate processes
        - Normal exit (voluntary)
        - Error exit (voluntary)
        - Fatal error (involuntary)
        - Killed by another process (involuntary)
        - Would a poorly written interrupt cause the last error?
            - No resumption?