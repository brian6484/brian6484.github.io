---
date: 2022-02-16 14:35:23
layout: post
title: Invoking the superclass version of a method
subtitle: Java 
description: Java
category: Java
tags:
  - Java
  - Head First Java
---

## What gives rise to needing the superclass version of method?

Q: What if you make a concrete subclass and you need to override a
method, but you want the behavior in the superclass version of the
method? In other words, what if you don’t need to *replace* the
method with an override, but you just want to *add* to it with some
additional specific code like more functionalities.

Ahhh...think about the meaning of the word *extends*. One area of good
OO design looks at how to design concrete code that’s **meant to be
overridden**. In other words, you write method code in, say, an abstract
class, that does work that’s generic enough to support typical concrete
implementations. But, the concrete code isn’t enough to handle all of the
subclass-specific work. So the subclass overrides the method and
extends it by adding the rest of the code. The keyword **super** lets you
invoke a superclass version of an overridden method, from within the
subclass.

```java
abstract class Report{
    //remember abstract class is to be extended 
    void runReport(){
        //blabla
    }
}

class BuzzReport extends Report{
    void runReport(){
        //call superclass version and do some sub-class stuff on it
        super.runReport();
        //blabla
    }
}
```

<img src="/assets/images/posts/java/Interface/11_interface1.png" title="제목" alt="아무거나" width="400"/> 



