---
date: 2022-05-05 14:35:23
layout: post
title: How long does object live?
description:
category: General Knowledge
tags:
  - General Knowledge
  - Head First Java
  - Java
---

## Introduction
Object's life depends 100% on the life of references that refer to it.

## If object's life depends on the reference variable's life, how long does variable live?

It depends if it is local variable or instance variable.

### Local variable
1) It lives only **within** the method that delcared the variable.
```java
public void read(){
    int s = 42;
    // s can only be used within this method
    // when this method ends, this variable dies completely
  }
```
In other words, the variable is **in scope** only within its own method. No other
code in the class or other classes can see it.

2) It lives as long as the object does.
```java
public class Hola{
    int size;
    public void setSize(int s){
        size = s;
    }
}
```
Variable 's' (in this case, it is a method parameter) is in scope only within the
setSize() method. But the instance variable named size is scoped to the life of the object.

#### Difference between scope and life
Life - local variable lives as long as its Stack frame is on the Stack. In other words,
until the method completes.

Scope - A local variable is in scope only within the method in which the variable
was declared. When its own method calls another, the variable is alive, but
not in scope until its method resumes. You can use a variable only when it
is in scope.

### Reference variable

The rules are the same for primitives and references. A reference variable
can be used only when it’s in scope, which means you can’t use an object’s
remote control unless you’ve got a reference variable that’s in scope.

An object is alive as long as there are live references to it. If a reference
variable goes out of scope but is still alive, the object it refers to is still
alive on the Heap. And then you have to ask...“What happens when the Stack
frame holding the reference gets popped off the Stack at the end of the
method?”

If that was the only live reference to the object, the object is now abandoned
on the Heap. The reference variable disintegrated with the Stack frame, so
the abandoned object is now, officially, toast. The trick is to know the point
at which an object becomes eligible for *garbage collection*.


#### How to rid object's reference variable 
3 ways to rid object's reference
1) reference goes out of scope permanently
```java
void go(){
    Life z = new Life();
    // reference z dies at the end of this method
  }
```

2) reference is assigned to another object
```java
Life z = new Life();
z = new Life();
//first object is abandoned when z references to a new object
```

3) reference is explicitly set to null
```java
Life z = new Life();
z = null;
//first object is abandoned when z is deprogrammed
```
