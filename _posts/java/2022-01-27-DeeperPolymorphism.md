---
date: 2022-01-27 14:35:23
layout: post
title: Deeper knowledge on Polymorphism
subtitle: Java 
description: Java
category: Java
tags:
  - Java
  - Head First Java
---
Deeper knowledge on Polymorphism:

## Introduction
Back in previous polymorphism article, we did:

```java
Wolf mywolf = new Wolf();

Animal myHippo = new Hippo();
```

But this time: can we do this?
```java
Animal myAnimal = new Animal();
```

Some classes **should not be instantiated**.

But how do we deal with this? We need an Animal class, for inheritance and
polymorphism. But we want programmers to instantiate only the less abstract
subclasses of class Animal, not Animal itself. We want Tiger objects and
Lion objects, not Animal objects.

We can stop instantiation (through *new* keyword) via marking the class as *abstract*.
The compiler will stop any code from creating an instance of that type.

You can still use that abstract type as a reference type. In fact, that’s a big
part of why you have that abstract class in the first place (to use it as a
polymorphic argument or return type, or to make a polymorphic array).

When you’re designing your class inheritance structure, you have to decide
which classes are *abstract* and which are *concrete*. Concrete classes are
those that are specific enough to be instantiated. A concrete class just means
that it’s OK to make objects of that type.


<img src="/assets/images/posts/java/Polymorphism/9_deeperpoly1.png" title="제목" alt="아무거나" width="400"/> 

Abstract class is **useless**, unless it is **extended**. With an abstract class, it’s the instances of a subclass of your abstract class
that’s doing the work at runtime. There is an exception to this—an abstract class can have static members

## Abstract methods
Besides classes, you can mark methods abstract, too. An abstract class
means the class must be *extended*; an abstract method means the method must
be *overridden*. You might decide that some (or all) behaviors in an abstract
class don’t make any sense unless they’re implemented by a more specific
subclass. In other words, you can’t think of any generic method
implementation that could possibly be useful for subclasses. What would a
generic eat() method look like?

An abstract method has no body!

```java
public abstract void eat();
//no method body
```

Because you’ve already decided there isn’t any code that would make sense
in the abstract method, you won’t put in a method body. So no curly braces—
just end the declaration with a semicolon.

If you declare an *abstract method*, you **MUST** mark the *class abstract* as
well. You can’t have an abstract method in a non-abstract class.
If you put even a single abstract method in a class, you have to make the class
abstract. But you can mix both abstract and non-abstract methods in the
abstract class.

## Point of abstract method?
What is the point of an abstract method? I thought the whole
point of an abstract class was to have common code that could be
inherited by subclasses.

Answer: Inheritable method implementations (in other words, methods with
actual bodies) are A Good Thing to put in a superclass. When it makes
sense. And in an abstract class, it often doesn’t make sense, because you
can’t come up with any generic code that subclasses would find useful.
The point of an abstract method is that even though you haven’t put in any
actual method code, you’ve still defined part of the protocol for a group
of subtypes (subclasses).

This is good for polymorphism. Remember, what you want is the ability to use a
superclass type (often abstract) as a method argument, return type, or
array type. That way, you get to add new subtypes (like a new Animal
subclass) to your program without having to rewrite (or add) new
methods to deal with those new types. Imagine how you’d have to change
the Vet class, if it didn’t use Animal as its argument type for methods.
You’d have to have a separate method for every single Animal subclass!
One that takes a Lion, one that takes a Wolf, one that takes a...you get the
idea. So with an abstract method, you’re saying, “All subtypes of this
type have THIS method” for the benefit of polymorphism.

## Must implement ALL abstract methods!

Abstract methods don’t have a body; they exist solely for polymorphism.
That means the first concrete class in the inheritance tree must implement all
abstract methods.

You can, however, pass the buck by being abstract yourself. If both Animal
and Canine are abstract, for example, and both have abstract methods, class
Canine does not have to implement the abstract methods from Animal. But as
soon as we get to the first concrete subclass, like Dog, that subclass must
implement all of the abstract methods from both Animal and Canine.

But remember that an abstract class can have both abstract and non-abstract
methods, so Canine, for example, could implement an abstract method from
Animal, so that Dog didn’t have to. But if Canine says nothing about the
abstract methods from Animal, Dog has to implement all of Animal’s abstract
methods.

When we say “you must implement the abstract method,” that means you must
provide a body. That means you must create a non-abstract method in your
class with the same method signature (name and arguments) and a return type
that is compatible with the declared return type of the abstract method. What
you put in that method is up to you. All Java cares about is that the method is
there, in your concrete subclass.

## Important
We are not making a new animal object. We are making a new *array* object of type animal.
Remember that you cannot make an instance of *abstract* type, but you *can* make an 
array object to hold that type.

```java
private Animal[] mylist= new Animal[5];
```

## Summary
>Remember, all
abstract methods MUST be implemented by the first concrete subclass
down the inheritance tree



