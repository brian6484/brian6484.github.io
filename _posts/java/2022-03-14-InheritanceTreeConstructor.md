---
date: 2022-03-14 14:35:23
layout: post
title: Role of superclass constructors in an object’s life
subtitle: Java 
description: Java
category: Java
tags:
  - Java
  - Head First Java
---

## Constructors in object's inheritance tree

> All the constructors in an object’s inheritance tree must run when you
make a new object.

That means every superclass has a constructor (because every class has a
constructor), and each constructor up the hierarchy runs at the time an object
of a subclass is created.

Saying *new* starts the whole constructor chain reaction. Even abstract classes have constructors. Although you can never say new
on an abstract class, an abstract class is still a superclass, so its constructor
runs when someone makes an instance of a concrete subclass.

The superclass constructors run to build out the superclass parts of the
object. Remember, a subclass might inherit methods that depend on
superclass state (in other words, the value of instance variables in the
superclass). For an object to be fully formed, all the superclass parts of itself
must be fully formed, and that’s why the superclass constructor must run. All
instance variables from every class in the inheritance tree have to be
declared and initialized. Even if Animal has instance variables that Hippo
doesn’t inherit (if the variables are private, for example), the Hippo still
depends on the Animal methods that use those variables.

When a constructor runs, it immediately calls its superclass constructor, all
the way up the chain until you get to the class Object constructor.

<img src="/assets/images/posts/java/Constructor/1_con.png" title="제목" alt="아무거나" width="400"/> 

## Explaining in stack
For example, let's say a Hippo extends Animal. So constructor of Hippo goes into the
stack frame. 

Then, Hippo() constructor invokes its superclass constructor, which **pushes** Animal()
constructor onto the top of the stack. So Animal() constructor is on top of Hippo() constructor.

Animal() constructor invokes its superclass constructor, which pushes Object() constructor
to the top of the stack. So code execution starts with Object() constructor, then Animal(),
then finally Hippo().

Remember:
>For an object to be fully formed, all the superclass parts of itself
must be fully formed, and that’s why the superclass constructor must run.

So superclass constructors must run first before subclass.

## How to call superclass constructor?

Through the **super** keyword. 

But so far, the compiler has been invoking super() when we didn't.

Compiler calls super() 
1) if you don't provide a constructor
2) if you do provide a constructor but do not put super() inside it

Also, very important that 
>The call to super() must be the first statement in each constructor!

This makes sense as like I said, for an object to be fully formed, all the superclass
parts of itself must be fully formed before.

However, there is 1 exception to this: invoking one overloaded constructor from another



## Superclass constructor with arguments
hat if the superclass constructor has arguments? Can you pass something in
to the super() call? Of course. If you couldn’t, you’d never be able to extend
a class that didn’t have a no-arg constructor. Imagine this scenario: all
animals have a name. There’s a getName() method in class Animal that
returns the value of the name instance variable. The instance variable is
marked private, but the subclass (in this case, Hippo) inherits the getName()
method. So here’s the problem: Hippo has a getName() method (through
inheritance) but does not have the name instance variable. Hippo has to
depend on the Animal part of himself to keep the name instance variable, and
return it when someone calls getName() on a Hippo object. But...how does
the Animal part get the name? 

The only reference Hippo has to the Animal
part of himself is through super(), so that’s the place where Hippo sends the
Hippo’s name up to the Animal part of himself, so that the Animal part can
store it in the private name instance variable.

```java
public class Hippo extends Animal{
    public Hippo(String name){
        //sends name up the Stack to the Animal constructor
        super(name);
    }
}
```




