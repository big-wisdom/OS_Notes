Roles of the operating system:
    Resource allocator
    manage conflicting requests
    Efficient use of hardware

What is an operating system?
    It's kinda fuzzy but mostly just the Kernel
    there's not a good universal definition
    fundamental purpose is to execute programs
    started as a grouping of commonly used functions (i.e. writing to disk, printing...) so that it didn't have to be put in
        every program
    Middleware goes between kernel and programs
        handles video
        surrounds the kernel



1-10
Interrupts
    two ways an interrupt can be raised
        Trap or Exception (Software on CPU)
        hardware (IO device)
    CPU has a physical interrupt line coming into it
    turn off all
    allow interrupts
    "mask" interrupts - Meaning only allow interrupts that will not create a conflict with presently running interrupts

Device Drivers run on CPU
Firmware funs on individual processors for things like disk or memory
PCI (Peripheral component interface)

Main memory 
    CPU has direct access
    Random
    Volatile
Secondary Storage
    Non-Volatile
        HDD
        SSD
        Magnetic tape
    Flash
    NVM
Tertiary
    Optical Disks
    magnetic tape
    Archivable stuff

Registers
Cache (near CPU)
Main memory

# 1-13 Computer System Architecture
## Types of processor Architectures:
* Single Processor
* Multi-Processor / Parallel
    * Throughput
    * Economy of scale
    * Increased Reliability
    * Types of multi-processing
        * Asymetric
            * There is a boss and workers
        * Symetric (SMP)
            * This is what everyone uses today
    * UMA vs NUMA:
        * Uniform Memory Access:
            * every processor takes the same amount of time to access memory
            * this doesn't scale very well
        * Non Uniform Memory Access:
            * Multiple groups of UMA
* Clustered
    * Storage Area Network (SAN) in the middle of several seperate machines
    * if you were to wipe out one computer, others still run
    * Increased realiability for real
        * Through "Graceful degradation"

* Dual Mode / Multi-Mode Operation
    * Solves the problem of multiple programs running both on memory and affecting memory
    * Divides CPU into a privilaged mode Kernel mode, and Hypervisor mode
        * Anything to do with IO is a good example of a "Privilaged" instruction
        * another priveleged instruction is the instruction to set an instruction as privilaged
    * there is User Mode and Kernel Mode (privilaged mode, supervisor mode... lots of names)
        * A user program is going along doing it's crap, it makes a system call, which creates an interrupt, and the OS calls a file writing code which executes in Kernel mode then switches back to user mode
        * The switch between modes is really time costly, could be tens of thousands of clock cycles
            * This makes batching better

    * Hyper-Visor Mode (Virtual Machine Manager):

    * There is something called a CPU Timer. When it hits 0 it creates an interrupt and the CPU switches to Kernel mode, looks at all of the processes, and decides which process gets to run next giving it a CPU Timer (Which is a privilaged instruction)
        * The thing that determines which process runs is the "Scheduler"
        * This is what prevents one process from dominating
        * Because of this, anytime you make a system call, the OS could decide on a different process to run instead of the one you just asked for

    * A Computer starts a boot loader which starts the OS
    * Vulnerabilites are when you try and run user code in Kernel mode

# 1-15 Multi-Programming / Multi-Tasking
Having more than one process in memory available to run
* Multi-Programming
    * Single CPU
        * "Jobs"
        * Switch while one is on IO

* Multi tasking doesn't wait for IO, it just switches quickly
    * switches using the CPU timer
* Proecess: In-memory, executed (active)
* Program: Compiled Source code (passive)
* Things the OS has to do
    * Process Management:
        * Create / delete memory
        * Schedule resume, suspend
        * Synchronize
        * Communication between processes
    * Memory Management
        * Control which process in memory or not
        * Allocate / deallocate space
        * track which memory is used by which process
    * File System Management
        * Logical view of IO device (like hdd or ssd)
        * create/delete files/folders 
        * organization of files/folders
        * files/folders manipulation 
        * backups
    * Mass storage
        * Works with long term storage of files
            * Mount/Unmount
            * Disk Scheduling
            * Partitioning
            * protection
    * Cache Management
        * data flow 
            * disk-> main memory-> cache-> registers
            * when some value is changed in registers, it has to be changed all the way back upstream to main memory
            * Then we decide if we want to go write that back to disk or not

* Virtualization
    * Emulation
        * MAME is a technology to emulate one architecture on another
    * Host OS
        * Environment for guest OS's
    * VM's run on top of that ^ and guest OS runs on those

# 1-17 Types of Computing
* Traditional Computing
    * Portal tower
    * Thin Clients
    * Remote accessability
    * Remote Computing
* Mobile Computing
    * This has become the primary method of computing, as in iPhones and mobile devices
    * Email, Messaging, web, social
* Distributed Systems
    * Physically seperate systems
    * Potentially Heterogeneous 
    * They might Share File System
* Client Server Computing
    * Client
        * Where the light computing is done
    * Server
        * Where the heavy work is done
* Peer to Peer Systems
    * There's no particular central network
    * this would be an example of a distributed system
    * Torrent is p2p
    * Napster was a torrent
* Cloud Computing
    * Software as a service (SaaS)
    * Platform as a service (PaaS)
        * Database
    * Infastructure as a service (IaaS)
        * Storage 
        * backup
        * Hard to tell the diff from (PaaS)
* Real-Time / Embedded Systems
    * Internet of Things
        * Edge Computing
            * Alexa n' Shit
    * Embedded Systems
        * device in the ski boot, aggie A sort of shit

# 1-24 OS Services
* OS Services
    * User Interface
        * Command Line
            * run in shells
                * shells can either have built in commands, or rely on other programs for their functionality
                    * Powershell has more built in commands and therefore slightly better performance
                    * bash uses other programs, and is therefore more extensible
        * GUI
            * WYSIWYGMOL (what you see is what you get more or less)
            * Desktop Metaphor
                * mouse, keyboard
                * files, folders, icon
                * set of services (API)
            * Xerox-palo Alto Research Pare
        * Touch
            * No Mouse, no keyboard
            * has graphics
            * virtual keyboard
            * voice assisted

    * Program Execution
    * I/O operations
    * File System
    * Communications
    * Error Detection & Recovery
    * Resource Allocations
    * Logging/Accounting

* System Calls
    * Interface between process & OS
    * API
        * win32
        * POSIX
        * Java
        * .NET

* User Application
    * When a user applicaiton makes a system call it passes arguments with several methods
        * Registers
        * Pass the address to a table you made
        * Place parameters on a stack (may or may not be the same as program execution stack)
            * give address of stack and stack frame

# 1-27 
* Why is code compiled OS specific?
    1. System Call interafce
    2. Executable Format
        * header and instructions can be different, mostly headers
* Linkers & Loaders
    * This applies to languages like c++ 
    * Source code -compiler-> Object File -linker-> .exe file -loader-> Process
        * Linker also reaches out to c++ standard library to mix code into the exe
* System Services
    * File Manipulation
    * Status
    * Programming Language Support
        * Debug / Performance
    * Program Loading and Execution
    * Communications
    * Background Services
    * Application Programs

# 1-29
* Mechanism 
    * How something is done (the thing)
    * this is having user and kernel mode
* Policy
    * How the mechanism is used
    * Policy is to only let kernel use kernel mode
* OS Implentation
    * Assembly
    * Algol
    * PL1 (stands for programming language 1 lol)
    * C, C++, Rust
        * Lowest level, still in assembly, meaning sensetive components are written in assembly
    * Monolithic Structure
        * Kernel
        * System Programs
        * monolithic because all main components are in the kernel (This is the much more popular version)
            * Scheduler
            * memory Management
            * File Systems
            * Networking
        * Layered Structure
            * Drawn with concentric circles, each layer can only communicate with adjacent layers
            * Ring 0: Hardward
            * Ring 1: 
            * Ring 2: OS Kernel
            * User Programs
    * Micro Kernel
        * Making the Kernel as small as possible, pushing everything else to user space
        
# 1-31
* Chronology of processes
    * Batch Systems
    * Intersecive (time-shared)
    * Processes
* Program is passive, Process is active
* Process is composed of 
    * Dynamic Memory
    * Global State, Resources
    * Executable code
* Process Control Block (PCB)
    * State
    * Program Counter
    * id number
    * CPU registers
    * Allocated memory
    * File Handles
    * Network Connections
* Process State Diagram
    * New -> Ready <-> Running -> Terminating
        * ready <- waiting <- running 
        * Waiting happens while making an I/O request, and during that, it's not even considered for scheduling
        * Schduler looks at ready
* Two kinds of processes
    * Objective: Maximize CPU / Devices (Mobile, sometimes objective is to be power efficient)
    1. CPU Bound
        * Heavily Uses CPU
        * Ex: Machine Learning
    2. I/O Bound
        * Mostly I/O Requests
        * Ex: Database processes
    * It can be a good think to run both types at the same time to maximize CPU / Devices
    
# 2-3
* Operations on processes
    * Creation
        * Process can create child processes
        * Resource Sharing
    * Execute
        * Both Concurrently 
        * Parent waits for child
    * Address Space
        * Dublicaiton of parent (fork)
        * New Image (execup)
    * Termination
        * Voluntarily
        * Parent can terminate child
            * if child is taking too many resources
            * if parent itself is terminating

# 2-5
* 

# 2-10 Interprocess Communication 
* Message passing systems
    * Send (p, message)
    * Recieve (p, message)
* Types of Links
    * Physical: Wire, Bus
    * Logical: buffers, Message passing
* Issues in IPC
    * Establish the link
    * How many processes, 2
    * How many links between proesses 
    * Capacity / Bandwidth (date/time)
        * Latency
    * uni or bi directional
    * Buffering
    * Blocking / Non-Blocking
* Direct Communication
    * Link Properties
        * one link, multiple
        * how link established
        * how many processes
* indirect Communication
    * Like a mailbox that both parties can look in except that it's not destructive, like you can have multiple people get the same message from the mailbox
* Synchronization
    * Communication can cause processes to be synchronized
    * If I know that this process is doing 'this', than this process is doing 'this'
    * Blocking
        * Send: sender is blocked until a message is recieved
        * Recieve: reciever is blocked until message sent
    * Non-Blocking
        * If you're non-blocking, there is a buffer somewhere. And you need something to do if the buffer is full
        * Send: Sender is never blocked
        * Recieve: Reciever get's available data
    * POSH Shared Memory
    * Mach message passing
    * Windows local procedure calls
    * All OS use Remote Procedure Calls (RPC)
        * Can also be used for a local computer
    * pipes, named pipes
    * Sockets
    * In java there is something called (RMI) Remote Method Invocation
    * in c# or .NET there is .NET remoting
* Copy and Pase is interprocess communicaiton
# Chapter 4 Multithreading
* Visibility
    * Code, data files, are all visible from all threads
    * Each thread has it's own stack

# 2-12
* Benefits of multithreading
    * it's faster to create a new thread than a new process
    * Responsiveness
    * Resource Sharing
    * Economy
    * Scalability
* Motivation
    * Single Process to perform multiple operations
* Concurrency VS. Parallelism
    * Concurrency is a system that can support more than one task and make progress on all of them
    * Parallelism is concurrency but tasks can be executed at the same time


# 2-14
* Two kinds of parallelism
    * Task: funcitonal decomposition
    * Data: data decomposition
* Amdahl's Law
    * How much can you speed up a program through parallelism?
* Logical Cores
    * When a memory stall occurs, due to having to go to main memory to get something the CPU can switch to a different pipeline of instructions
    * Both pipelines are probably running the in same mode. Either user or kernel
* Global Interpreter Lock (python)

# 2-19 Threading 
* Threading libraries
    * Pthreads (mac)
    * WindowsThreads (windows duh)
        * Kernel Threads
    * JavaThreads
        * How to:
            * extend Thread 
            * implement Runnable
                * then pass that object to a thread
                * start the thread 

# 2-24
* Thread Pools
    * Fork-join parallelism 
        * OpenMP C++/ Fortran
            * Specify using directives
            * Intel Thread Building Blocks (TBB) 
        * IOS - Grand Central Dispatch 
            * create dispatches like this ^{} that get put into a queue of sorts, then set that queue to run either in parallel or serially.
* Problems with multithreading
    * Signal Handling: Which thread gets the signal? If I hit ctrl+c which process get's terminated
    * Thread Cancelation
        * Voluntary - When the job is done
        * Deferred - Someone else controlling the variable that your while loop depends on
        * Asynchronous (involuntary) (non-consentual)