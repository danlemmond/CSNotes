# OS Notes 8/23

## Kernels
    Monolithic vs. Microkernel
    Handling of the filesystems and the way the system accesses memory.
    Way the program interacts with privileges and permissions

## Monolithic
    Entire kernel is a large process, single address space
    Kernel services execute in kernel address space
    Pros: Fast, easy to implement
    Cons: 
        - Huge Kernel
        - No protection between kernel components
        - Complex dependencies, not easily extensible

## Microkernel
    Kernel broken down to separate processes(aka servers)
    Servers kept separate and run in different address spaces (safer)
    Communication is done via message passing
        - Servers communicate through IPC (Inter-process Communication)
    Pros:
        - Modular design, easily extensible
        - Easy to maintain
        - More reliable and secure
    Cons: Performance loss, complicated process 

## History of Operating Systems
    First Gen 1945 - 1955
        - Vacuum tubes, plug boards
    Second Gen 1955 - 1965
        - Transistors, Batch Systems
    Third Gen 1965 - 1980
        - ICs and multiprogramming
            - Multiprogramming - Storing programs in memory for rapid access
    Fourth Gen 1980 - Present
        - Personal Computers, LSI (Large Scale Integration)
    Present Next 5 - 10 Years
        - Mobile Devices
        - Multicore Computers (Many core sounds ~~dumb~~ incorrect.)
        - GPU operations != CPU operations and they aren't even remotely close to equivalent

### Literally Moore's Law

## Computer Hardware Overview
    CPU: Data processing
    Memory: volatile data storage
    Disk: Persistent data storage
    NIC: Inter-machine Communication
    Bus: Intra-machine Communication

## CPU
    Components:
        - ALU or Arithmetic Logic Unit
        - CU or Control Unit
        - Fetch, Decode, Execute
    Clock Rate
        - The speed at which a CPU is running
    Data storage: mem access is *slow*
        - General Purpose: EAX, EBX, etc.
        - Special-purpose Register: PC, SP, IR
    Parallelism
                F       D       E
        t1 =    1
        t2 =    2       1
        t3 =    3       2       1
        Parallelism in the CPU exists as a way to simultaneously fetch, decode, and execute instructions.

## Multi-core CPUs
    Multiple CPUs on a single chip
    See Slide Diagram

## Memory
    Typical Access Time:
        - 1 nsec       = Registers          = <1 kb
        - 2 nsec       = Cache              = 4mb
        - 10 nsec      = Main Memory        = 512 - 2048mb
        - 10 msec      = Magnetic Disk      = 200 - 1000 gb
        - 100 sec      = Magnetic Tape      = 400 - 800 gb
    Doubling Rates Vary:
        - As CPUs get faster, DRAM can't keep up. 
        - Caching is used to divide processes into pieces in order to discriminate based upon usage. Highly used is cached, lowly used is not.

## CPU Caches
    L1 Cache:
        - Inside CPU, feeds decoded instructions to CPU execution engine
    L2 Cache:
        - Inside or outside CPU, holds megabytes of recently used memory words, (1-2 clock cycles)
    L3 Cache:
        - Outside CPU, LLC - Last Level Cache

## Cache Management
    When to put a new item into the cache?
        - 
    Which cache line to put the new item in?
        - 
    Which item to remove from the cache when a slot is needed?
        - 
    Where to put a newly evicted item in the larger memory?
        - 
    When to write dirty item back to memory?
        - 

## Memory Management
    Multiprogramming
        - Accomodate multiple processes in main memory
        - How to *protect* the programs from one another and the kernel from them all?
            - Processes should not reference memory locations in another process without permission.
        - How to handle *relocation*?
            - If P4 has higher priority, we can terminate P2
            - 

    Virtual memory space/address -> Physical memory space/address

## Hard Disks
    A stack of platters, a surface with a magnetic coating
    Typical numbers (depending on disk size):
        - 500 to 2,000 tracks per surface
        - 32 to 128 sectors per track
            - A sector is the smallest unit that can be read or written
    Originally, all tracks have the same number of sectors:
        - Constant bit density: Record more sectors on the outer tracks (modern disks)

## Magnetic Disk Characteristics
    Disk head: Each side of a platter has separate disk head
    Read/write is a three stage process:
        - Seek Time
        - Rotational Latency
        - Transfer Time
    Average seek time as reported by the industry:
        - Typically between 8 and 15ms
        - Sum of the time for all possible seek / total number of possible seeks
    Due to locality of disk reference
        - Actual average seek time may only be 25 to 33% of advertised number

## CPU vs. Hard Disks
    CPU
        - Cache Reuse -> Temporal Locality
        - Easy to switch between sharing parties -> fine grain, overhead sensitive
        - Usually multiple CPUs -> Load Balancing
        - Multiple Execution Modes -> Energy Saving
    HDDs
        - Almost no data reuse, but faster to read adjacent data -> Spatial locality
        - Expensive to switch between sharing parties -> Coarse grain
        - Striping or replication required if using multiple disks -> Coordination

## I/O Devices
    Device Controller
        - To provide a simple interface of device control to the OS
        - Physically controls the device: accepts commands from OS, and carries them out
    Device driver:
        - Software that talks to a controller, giving it commands and accepting responses
        - Every controller has a small number of registers: A disk controller might have registers for specifying disk address, direction (r/w), etc.

