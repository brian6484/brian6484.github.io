---
date: 2022-02-03 14:35:23
layout: post
title: Object Class polymorphism
subtitle: Java 
description: Java
category: Java
tags:
  - Java
  - Head First Java
---

## Every class in Java extends class Object

Class Object is the mother of all classes. It is the superclass of everything.
Every class you write extends Object.

Any class that doesn’t explicitly extend another class, implicitly extends
Object.

For example:
```java
public class Dog extends Object{
    
}
```

But wait a minute, Dog already extends something, Canine. That’s OK. The
compiler will make Canine extend Object instead. Except Canine extends
Animal. No problem, then the compiler will just make Animal extend Object.

## Object is a non-abstract class
Because it has method implementation code that all classes can inherit from and use, without
having to override them.

## SOME methods in Object can be overriden
Only some, but the rest are marked as *final*. Book encourages to override
hashCode(), equals() and toString().

## Purpose of Object class
1) Act as polymorphic type for methods that need to work on a class that I make

2) Provide real method code that all objects in Java need, at runtime (this is possible cuz
putting that code in Object means all classes can inherit them)

3) for threading

## We can't make our methods take and return Object type
If we do that, it defeats the whole point of “type-safety,” one of Java’s greatest protection
mechanisms for your code. With type-safety, Java guarantees that you
won’t ask the wrong object to do something you meant to ask of another
object type. Like, ask a Ferrari (which you think is a Toaster) to cook
itself.

But actually, you don’t have to worry about that fiery Ferrari scenario,
even if you do use Object references for everything. Because when
objects are referred to by an Object reference type, Java thinks it’s
referring to an instance of type Object. And that means the only methods
you’re allowed to call on that object are the ones declared in class
Object!

```java
Object o= new Ferrari();
//won't work
o.goFast();
```

Because Java is a strongly typed language, the compiler checks to make
sure that you’re calling a method on an object that’s actually capable of
responding. In other words, you can call a method on an object reference
only if the class of the reference type actually has the method.

## Using polymorphic reference of type Object
```java
ArrayList<Object> list = new ArrayList<>();
Dog bitch = new Dog();
list.add(bitch);

//won't compile
Dog d = list.get(0);
```

It will not compile because when we use ArrayList<Object>, the get() method returns
type Object. The compiler only knows that the object inherits from Object but does
not know it is a Dog type.

Everything comes out of an ArrayList<Object> as a reference of type
Object, regardless of what the actual object is or what the reference type
was when you added the object to the list

<img src="/assets/images/posts/java/Polymorphism/10_objectpoly1.png" title="제목" alt="아무거나" width="400"/> 

When an object is referenced by a variable declared as
type Object, it can’t be assigned to a variable declared with the actual
object’s type (like Dog). And we know that this can happen when a return type or
argument is declared as type Object, as would be the case, for example,
when the object is put into an ArrayList of type Object using
ArrayList<Object>.

## Summary
> The compiler decides whether you can call a method based on the reference type, not the
actual object type.

**The method you are calling on a *reference* must be in the class of that reference type.
It does not matter what the actual object is**.

For example, object.hasCode() is a legit method in that Object class. But object.bark
is not.

Even if you know the object is capable,
the compiler sees it only as a generic Object. For all the compiler knows,
you put a Button object out there. Or a Microwave object. Or some other
thing that really doesn’t know how to bark.

The compiler checks the class of the reference type—not the object type—to
see if you can call a method using that reference
