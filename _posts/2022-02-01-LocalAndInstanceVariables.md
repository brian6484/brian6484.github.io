---
date: 2022-02-01 14:35:23
layout: post
title: Difference between local and instance variables
description:
category: Java
tags:
  - Java
  
* Difference between local and instance variable: 

Instance variables are declared inside a class but not within a
  method.
```java
class Horse {
  private double height = 15.2;
  private String breed;
  // more code...
}
```
Local variables are declared within a method and **MUST** be in initalised.

<img src="/assets/images/posts/general%20knowledge/1.png" title="제목" alt="아무거나"/> 
<img src="/assets/images/posts/2.png" title="제목" alt="아무거나"/> 

BTW, instance variables, if unitialised, are assigned values by default to 0 and false.

* How about method parameters?

Method parameters are virtually the same as local variables—they’re
  declared inside the method (well, technically they’re declared in the
  argument list of the method rather than within the body of the method, but
  they’re still local variables as opposed to instance variables). But
  method parameters will never be uninitialized, so you’ll never get a
  compiler error telling you that a parameter variable might not have been
  initialized.
  Instead, the compiler will give you an error if you try to invoke a method
  without giving the arguments that the method needs. So parameters are
  always initialized, because the compiler guarantees that methods are
  always called with arguments that match the parameters. The arguments
  are assigned (automatically) to the parameters




