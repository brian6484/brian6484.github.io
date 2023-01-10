---
layout: post
title: What is thread in Java? (feat. process)
category: Java
tags:
  - Java
  - Head First Java
---


## Process
<img src="/assets/images/posts/java/Thread/process1.png" title="제목" alt="아무거나" width="400"/> 
It is an instance of program is loaded into memory and runs. 
It is a unit of work that allocates system resources from OS.
Each process is allocated an independent memory area (code,data,
stack,heap) and has at least 1 thread (main thread). Each process
also runs in a separate address space so to access variables,
etc, they need to *communicate*

## Thread
A unit of multiple execution flows runs within a process. 
It is a unit of execution that uses the resources allocated to a given process.

Difference between process and thread is that each thread is given only 
a separate stack within the process. Code, data and heap space are 
shared. So multiple processes can be executed can be executed simultaneously
while sharing resources in 1 process

## Multi-process
A single application consists of multiple processes.
Advantages:
* Failure of one process does not affect other processes
Disadvantages
* Overhead in Context Switching: Each process is allocated an independent memory area (shared memory x), so when context switching occurs, all data in the cache must be reset and cache information received again.
* Context switching: When processing while working while rotating several processes in the CPU, the running process waits and keeps the state (Context) of the process
* Difficult and complex communication techniques between processes

## Multi-thread
An application is composed of multiple threads, each thread performing one test.
A web server is a typical multi-threaded application.
Advantages:
* Increased system resource efficiency: Reduced system calls for creating processes and allocating resources.
* Reduced system processing cost: Reduced system resource consumption (memory sharing outside of Stack). Context switching is fast because the amount of work between threads is small (only stack is processed)
* Simple communication method, shortened response time: Less communication burden because threads within a process share all memory except stack
Disadvantages:
* Debugging tricky
* In the case of multi-threading, synchronization problems may occur
* If one thread fails, the entire process is affected.
