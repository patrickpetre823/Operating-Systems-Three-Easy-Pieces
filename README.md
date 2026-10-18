# Operating-Systems-Three-Easy-Pieces
Short summaries of the book "Operating Systems: Three Easy Pieces". This is just for personal use. Writing & summarizing helps to memorize what I read and also I can come back in the future and read my summary.

The book and additional information can be found here: https://pages.cs.wisc.edu/~remzi/OSTEP/?theme=2019%2F1000

## Introduction

This chapter gives a brief overview of the topics covered in this book. There are 3 main objectives of an OS and these are the main topics covered in different chapters.

1. **`Virtualization`**
   The OS is responsible of virtualization of the CPU and RAM for programs. Thus programs can run simultaneously and 
2. **`Concurrency`**
   Multiple threads can execute concurrently.
3. **`Persistence`**
   File systems store data permanently on SSDs or hard drives

   Key takeaway: An operating system manages CPU time, RAM, and storage, provides simple interfaces, and ensures that multiple programs can work together efficiently and securely.


## Virtualization

### Process
The first question is: What is a process? A process is simply a running program.

The second question is: How can the OS give the illusion of many CPUs when only a few exist? The answer is **`time sharing`**. Run one process, stop it, run another, and so on. This costs a bit of performance. The counter part is space sharing. This divides a resource partially, for example storage. 

How does this work?
->Mechanisms & policies


To fully understand a process, you have to understand the machine state. The machine state describes everything that is needed to execute a program. 
This usually consists of: 
- memory (The memory a process can address is called address space)
- registers (Some special registers are program counter PC or Instruction counter IP. They tell us which instruction of the program will execute next)
- I/O information



### Process API
- Create
- Destroy
- Wait
- Miscellaneous Control (for example stopping a process and resume it after a while)
- Status
- more

### Process creation
To start a process the OS needs to load programs code and static data into memory, that is the address space (Nowadays performed lazily, not everything at once)
Some of the address space must be allocated to the programs **`run-time stack`** (local variables, functions etc.) and **`heap`** (dynamic reserved memory).
Then the OS usually does some initialization related to I/O, for example on UNIX, every process gets 3 file descriptors.
Finally the OS starts the program, typically by jumping to main(). Thus transferring control to the CPU.

### Process States
A process can be in one of 3 different states. 
Running, means a process is currently running on a processor.
Ready, means a process is ready to run, but the OS has chosen to not run it at the moment. 
Blocked means a process has performed some kind of operation that makes it not ready to run. For example, when a process initiates an I7O request to a disk, it becomes blocked.

### Data Structures
To manage all of these different topics, the OS needs it own data structure to manage all of it. 
The OS has a list of all the processes in a data structure called Process Control  Block (PCB). In this list there a different information's about a process, for example Process ID, State etc.
This is important. If the OS chooses to pause a process and resume it afterwards, it needs all of this information to resume it from the point it got stopped. This is called **`Context switching`**.

### Direct Execution
The main question is: How does the OS achieve virtualization and keep performance without loosing control. 
The basic technique is called **`limited direct execution`**. This basically just means "run the program directly on the CPU". This intruduces some problems tha we need to solve.

Problem 1: Restricted Operations
Direct execution has the benefit of performance but raises the problem of restricted operation. For example a process may want to perform some kind of I/O request to a disk. 
To manage this, we introduce a new processor mode, called **`user mode`**. Code that runs in this mode is restricted to what it can do. In contrast to user mode is **`kernel mode`**, where code 
has privileged access to hardware and system ressources.
If an application want to access privileged services while running in user mode, it makes a **`system call`**. This will hand the OS control of this specific service request. For this use case, the OS keeps a list of addresses, called the  **`Trap table`**. The addresses point to kernel functions, for example "&keyboard_handler". After it is completed, the OS calls a **`return-from-trap`**.
