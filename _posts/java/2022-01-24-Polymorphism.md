---
date: 2022-01-24 14:35:23
layout: post
title: Polymorphism
subtitle: Java 
description: Java
category: Java
tags:
  - Java
  - Head First Java
---
Polymorphism:

## Introduction
Let's first step back and look at how we declare a reference and create an object:

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

Important note is that reference type AND the object type are the same. In this case,
both are type Dog.


## Here comes polymorphism

However, with polymorphism, the **reference type** and the **object type** can be
**different**.

```java
Animal bitch = new Dog();
```

Here, reference variable type is Animal but the object created is Dog.

When you declare a reference variable, any object that passes the IS-A test
for the type of the reference can be assigned to that variable. In other words,
anything that *extends* the declared reference variable type can be assigned to
the reference variable. This lets you do things like make polymorphic
arrays.


<img src="/assets/images/posts/java/Polymorphism/5_poly.png" title="제목" alt="아무거나" width="400"/>

## Polymorphic arguments(to a method) and return types

You can also have polymorphic arguments and return types.

If you can declare a reference variable of a supertype, say, Animal, and
assign a subclass object to it, say, Dog, think of how that might work when
that reference is an argument to a method...

<img src="/assets/images/posts/java/Polymorphism/6_poly2.png" title="제목" alt="아무거나" width="400"/> 

## 3 ways to prevent a class from being subclassed

1) Although there is no such things as *private* class, a class can be non-public (what you get if you don’t declare
   the class as public). A non-public class can be subclassed only by
   classes in the same package as the class. Classes in a different package
   won’t be able to subclass (or even use, for that matter) the non-public
   class.
2) Through keyword modifier **final**. A final class means that it’s the end of the inheritance
   line. Nobody, ever, can extend a final class.
3) if a class has **only private** constructors

A note on keyword **final** is that typically, you won’t make your classes final. But if you need security
—the security of knowing that the methods will always work the way that
you wrote them (because they can’t be overridden), a final class will
give you that. A lot of classes in the Java API are final for that reason.
The String class, for example, is final because, well, imagine the havoc
if somebody came along and changed the way Strings behave!

If you want to protect a specific *method* from being overridden, mark
the method with the final modifier. Mark the whole class as final if you
want to guarantee that none of the methods in that class will ever be
overridden.

## Common mistakes with poly

<img src="/assets/images/posts/java/Polymorphism/7_poly_mistake1.png" title="제목" alt="아무거나" width="400"/> 

1) Arguments must be the same, and return types must be
   compatible.

The contract of superclass defines how other code can use a method.
Whatever the superclass takes as an argument, the subclass overriding
the method must use that same argument. And whatever the superclass
declares as a return type, the overriding method must declare either the
same type or a subclass type. Remember, a subclass object is
guaranteed to be able to do anything its superclass declares, so it’s safe
to return a subclass where the superclass is expected.


<img src="/assets/images/posts/java/Polymorphism/8_poly_mistake2.png" title="제목" alt="아무거나" width="400"/>

2) The method can’t be less accessible.

That means the access level must be the same, or friendlier. You can’t,
for example, override a public method and make it private.





