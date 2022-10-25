---
layout: post
title: try/catch finally flow control
subtitle: Java 
description: Java
category: Java
tags:
  - Java
  - Head First Java
---
## try/catch flow control

<img src="/assets/images/posts/java/TryCatch/trycatch1.png" title="제목" alt="아무거나" width="400"/>

Rest of the try block does not run if it fails and goes straight to
the catch block.

## finally
A finally block is where you put code that must run regardless of an
exception.

```java
try {
turnOvenOn();
x.bake();
} catch (BakingException e) {
e.printStackTrace();
} finally {
turnOvenOff();
}
```

Without finally, you have to put the turnOvenOff() in both the try and the
catch because you have to turn off the oven no matter what. A finally
block lets you put all your important cleanup code in one place instead of
duplicating it like this:

```java
try {
turnOvenOn();
x.bake();
turnOvenOff();
} catch (BakingException e) {
e.printStackTrace();
turnOvenOff();
}
```

If the try block fails (an exception), flow control immediately moves to the
catch block. When the catch block completes, the finally block runs. When
the finally block completes, the rest of the method continues on.

If the try block succeeds (no exception), flow control skips over the catch
block and moves to the finally block. When the finally block completes, the
rest of the method continues on.

If the try or catch block has a *return* statement, finally will **still run**!
That is surprising to me. Flow jumps to the finally, then back to the return.





