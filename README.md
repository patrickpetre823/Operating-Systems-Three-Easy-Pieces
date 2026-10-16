# Operating-Systems-Three-Easy-Pieces
Short summaries of the book "Operating Systems: Three Easy Pieces". This is just for personal use. Writing & summarizing helps to memorize what I read and also I can come back in the future and read my summary.

## Introduction

This chapter gives a brief overview of the topics covered in this book. There are 3 main objectives of an OS and these are the main topics covered in different chapters.

1. Virtualization
   The OS is responsible of virtualization of the CPU and RAM for programs. Thus programs can run simultaneously and 
2. Concurrency
   Multiple threads can execute concurrently.
3. Persistence
   File systems store data permanently on SSDs or hard drives

   Key takeaway: An operating system manages CPU time, RAM, and storage, provides simple interfaces, and ensures that multiple programs can work together efficiently and securely.


## Virtualization

### Process
The first question is: What is a process? A process is simply a running program. 
The second question is: How can the OS give the illusion of many CPUs when only a few exist? The answer is time sharing. Run one process, stop it, run another, and so on. This costs a bit of performance. The counter part is space sharing. This divides a resource partially, for example storage. 

How does this work?

Mechanisms & policies


### Process API

   
