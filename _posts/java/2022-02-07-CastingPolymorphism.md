---
date: 2022-02-07 14:35:23
layout: post
title: Casting Polymorphism
subtitle: Java 
description: Java
category: Java
tags:
  - Java
  - Head First Java
---

# Introduction
>Just remember that the compiler checks the class of the reference
variable, not the class of the actual object at the other end of the
reference

Previously, in Object Class Polymorphism, we wanted to get a Dog from ArrayList<Object>
that has Dog methods. But we couldn't because method that we can use is based on the
reference type, not the object type.

However, we can **cast** and object reference *back* to its real type.

## Casting

```java
Object o = list.get(index);
//cast object back to the Dog type
Dog d = (Dog) o;

//no compile issue
d.roam();
```

If we are sure that the object is really a Dog, we can make a new Dog reference
by coping the Object reference and *forcing* that copy to go into the Dog reference
variable, using a cast (Dog). We can now use the new Dog reference to call Dog methods.

If you are not sure of its type, we can use *instanceof* operator. If it is wrong when we 
try casting, we get a ClassCastException at runtime.

```java
if(o instancof Dog){
    Dog d = (Dog) o;
  }
```

