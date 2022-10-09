---
date: 2022-03-17 14:35:23
layout: post
title: How to call a constructor from another constructor within the same class (not from subclass)
subtitle: Java 
description: Java
category: Java
tags:
  - Java
  - Head First Java
---

## Invoking overloaded constructor from another constructor within the same class

[stack overflow](https://stackoverflow.com/questions/285177/how-do-i-call-one-constructor-from-another-in-java)
explained it well but let's look at it more closely.

It is through the "this()" keyword.

<img src="/assets/images/posts/java/Constructor/2_con.png" title="제목" alt="아무거나" width="400"/> 

```java
class Temp
{
    // default constructor 1
    Temp()
    {
        System.out.println("default");
    }
 
    // parameterized constructor 2
    Temp(int x)
    {
        // invokes default constructor
        this();
        System.out.println(x);
    }
 
    // parameterized constructor 3
    Temp(int x, int y)
    {
        // invokes parameterized constructor 2
        this(5);
        System.out.println(x * y);
    }
 
    public static void main(String args[])
    {
        // invokes parameterized constructor 3
        new Temp(8, 10);
    }
}
```

Output is default -> 5 -> 80. Remember even though subclass constructor is invoked first,
but it is the superclass constructor that is on top of Stack and thus is executed first.
If you don't remember, relook at previous post

## Constructor Chaining to other class using super() keyword 

```java
class Base
{
    String name;
 
    // constructor 1
    Base()
    {
        this("");
        System.out.println("No-argument constructor of" + 
                                           " base class");
    }
 
    // constructor 2
    Base(String name)
    {
        this.name = name;
        System.out.println("Calling parameterized constructor"
                                              + " of base");
    }
}
 
class Derived extends Base
{
    // constructor 3
    Derived()
    {
        System.out.println("No-argument constructor " + 
                           "of derived");
    }
 
    // parameterized constructor 4
    Derived(String name)
    {
        // invokes base class constructor 2
        super(name);
        System.out.println("Calling parameterized " + 
                           "constructor of derived");
    }
 
    public static void main(String args[])
    {
        // calls parameterized constructor 4
        Derived obj = new Derived("test");
 
        // Calls No-argument constructor
        // Derived obj = new Derived();
    }
}
```

Output is Calling parameterized constructor of base -> Calling parameterized constructor of derived

