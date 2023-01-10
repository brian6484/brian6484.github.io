---
layout: post
title: What is deadlock? 
category: Java
tags:
  - Java
  - Head First Java
---


## Deadlock
In multi-threaded programming, locks are obtained through 
synchronization to prevent resource use in multiple places.
Two or more threads are waiting to acquire a lock, and the 
threads holding the lock are also blocking each other while 
waiting for another lock. (e.g. operation1 has lock1 and
waits to acquire lock2, operation2 has lock2 and waits to 
acquire lock1)

It causes an infinite circular waiting time until each thread's work
is finished (i.e. lock is released)

```java
Thread 1  locks A, waits for B
Thread 2  locks B, waits for A
```

## Solution
1) Avoid circular wait - No deadlocks will happen if all locks
are always acquired in the same order. 

e.g. if both operation1 and operation2
are occupied by lock1, followed by lock2, then no problem. But
limitation is we may not know the order of locks
2) Lock timeout - amount of time a thread waits to acquire a lock

If the lock is not acquired by the timeout period, this thread relinquishes the lock.
Even if you hold the lock for a long time to process a task, 
you may give up due to the lock timeout.
Limitation that a timeout cannot be set for entering a *sync block*. For this you need to create a custom lock class or use java.util.concurrency (Thread safe package).

3) Set priorities to preoccupy resources 
4) Remove mutual exclusion conditions 
