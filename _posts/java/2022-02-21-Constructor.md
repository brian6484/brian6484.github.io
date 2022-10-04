---
date: 2022-02-21 14:35:23
layout: post
title: Constructor
subtitle: Java 
description: Java
category: Java
tags:
  - Java
  - Head First Java
---

## Introduction - how are objects created?

Let's go back to how objects are created. [polymorphism post](https://brian6484.github.io/java/2022/01/24/Polymorphism.html)

```java
//1) declare reference variable
// Tells the JVM to allocate space for a reference variable. The reference
//variable is, forever, of type Dog. In other words, a remote control that
//has buttons to control a Dog, but not a Cat or a Button or a Socket.

    Dog bitch = new Dog();

//2) create object
// Tells the JVM to allocate space for a new Dog object on the garbage 
// collectible heap
    Dog bitch = new Dog();

//3) Link the object and reference
// Assigns the new Dog to the reference variable myDog. In other words,
  program the remote control.
  
    Dog bitch = new Dog();
```

At step 2, it looks like we are calling a method named Dog()
because of the parentheses. Nope, it is the Dog *constructor*

## Constructor 

A constructor does look and feel a lot like a method, but it’s not a method.
It’s got the code that runs when you use the keyword *new*. In other words, the code that
runs when you instantiate an object.

The only way to invoke a constructor is with the keyword new followed by
the class name. The JVM finds that class and invokes the constructor in that
class. (OK, technically this isn’t the only way to invoke a constructor. But
it’s the only way to do it from outside a constructor. You can call a
constructor from within another constructor, with restrictions, but we’ll get
into all that later in the chapter.)

> Every class you write has a constructor, even if you don't write
it cuz the compiler writes it for you

No return type needed for constructor.
```java
// no return type like void, Long, etc
public Duck(){
    //constructor code
  }
```

### Why is constructor useful?
The key feature of a constructor is that it runs before the object can be
assigned to a reference. That means you get a chance to step in and do things
to get the object ready for use. In other words, before anyone can use the
remote control for an object, the object has a chance to help construct itself.

> Constructor gives you a chance to step in the middle of *new*

## Overloading constructor 
If you have more than one
constructor in a class, it means you have overloaded constructors.

## Precautions
The compiler gets involved with
constructor-making only if you don’t say anything at all about constructors.

>If you write a constructor that takes arguments and you still want a no-arg constructor, you’ll have to build the no-arg constructor yourself!

As soon as you provide a constructor, ANY kind of constructor, the compiler
backs off.

>If you have more than one constructor in a class, the constructors MUST
have different argument lists.

The argument list includes the **order** and types of the arguments. As long as
they’re different, you can have more than one constructor. You can do this
with methods as well, but we’ll get to that in another chapter.

For example,
```java
// different order even tho same args, so fine
public Dog(int size, boolean True){
    
  }
public Dog(boolean True, int size){
    
  }
```

