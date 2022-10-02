---
date: 2022-01-10 14:35:23
layout: post
title: Difference between local and instance variables
description:
category: Java
tags:
  - Java
  - Head First Java
  
## Difference between local and instance variables: 

Instance variables are declared inside a class but not within a
  method.
```java
class Horse {
    //instance variables
  private double height = 15.2;
  private String breed;
  // more code...
}
```
Local variables are declared within a method and **MUST** be in initalised.

<img src="/assets/images/posts/java/DiffBetweenLocalAndInstanceVariables/1.png" title="제목" width="200"/>

BTW, instance variables, if uninitialised, are assigned values by default to 0 and false.
So just initialise instance variables too!

## How about method parameters?

<img src="/assets/images/posts/java/DiffBetweenLocalAndInstanceVariables/2.png" title="제목" width="200"/> 

Method parameters are virtually the same as local variables—they’re
  declared inside the method (well, technically they’re declared in the
  argument list of the method rather than within the body of the method, but
  they’re still local variables as opposed to instance variables). 

But method parameters will never be uninitialized, so you’ll never get a
  compiler error telling you that a parameter variable might not have been
  initialized.
  Instead, the compiler will give you an error if you try to invoke a method
  without giving the arguments that the method needs. So parameters are
  always initialized, because the compiler guarantees that methods are
  always called with arguments that match the parameters. The arguments
  are assigned (automatically) to the parameters




