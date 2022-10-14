---
date: 2022-05-09 14:35:23
layout: post
title: Meaning of static variable and method and how to initialise them
subtitle: Java 
description: Java
category: Java
tags:
  - Java
  - Head First Java
---

## Intro 
>Methods in the Math class don’t use any instance variable values. And because the methods are
“static,” you don’t need to have an instance of Math. All you need is the Math class.

Java is object-oriented, but once in a while you have a special case,
typically a utility method (like the Math methods), where there is no need to
have an instance of the class. The keyword **static** lets a method run
**without any instance of the class**. A static method means “behavior not
dependent on an instance variable, so no instance/object is required. Just the
class.”

<img src="/assets/images/posts/java/Static/1_static.png" title="제목" alt="아무거나" width="400"/>


## Calling static method (using class name)
So for normal non-static methods, we have been using a reference
variable name.

```java
Song t2 = new Song();
t2.play();
```

But for static method, we call it via a class name.

```java
Math.min(4,6);
```

## Similarity between class with static method and abstract class
Often (although not always), a class with static methods is
**not meant to be instantiated**. This is similar to **abstract class**
that does not allow to say "new" on that class type. In more technical
terms, it is impossible to instantiate an abstract class.

But you can restrict other code from instantiating a non-abstract class by
marking the constructor private. Remember, a method marked private
means that only code from within the class can invoke the method. A
constructor marked private means essentially the same thing—only code
from within the class can invoke the constructor. Nobody can say “new” from
outside the class. That’s how it works with the Math class, for example. The
constructor is private; you cannot make a new instance of Math. The
compiler knows that your code doesn’t have access to that private
constructor.

This does not mean that a class with one or more static methods should never
be instantiated. In fact, every class you put a main() method in is a class with
a static method in it!

## Static methods can't use non-static (instance) variables and methods
Static methods run without knowing about any particular instance of the static
method’s class. There might not even
be any instances of that class. Since a static method is called using the class
(Math.random()) as opposed to an instance reference (t2.play()), a static
method can’t refer to any instance variables of the class. The static method
doesn’t know which instance’s variable value to use.

Also, non-static *methods* use instance variable state to affect the
behaviour of the method.

For example,

```java
public class Duck {
  private int size;

  public static void main(String[] args) {
    //this is not static because we don't know which duck and whose size
    System.out.println("size of duck is" + size);

    //invoking non-static method doesnt work because it uses instance
    //variable (size)
    System.out.println("size of duck is"+ getSize());
  }

  public int getSize() {
    return size;
  }
}
```

Error is "non-static variable size cannot be referenced from a 
static context"

> If you try to use an instance variable from inside a static method, the compiler thinks, “I don’t know
which object’s instance variable you’re talking about!” If you have ten Duck objects on the heap, a
static method doesn’t know about any of them

Even if a non-static method does not use **any** instance variable and
you call that method from a static method, it still does not work.

## Very important: Static variable value is same for ALL instances of class
I have been very confused about this so let's clear this up.

For example, we want to count number of Duck instances being created.
Maybe an instance variable that is set to increment in the constructor?

Will this work??
```java
class Duck{
    int duckCount=0;
    public Duck(){
        duckCount++;
    }
}
```
NOOO because duckCount is an **instance variable** and it starts
at 0 for each Duck. This constructor just sets duckCount to 1 each
time a Duck instance is made.

What we need is a static variable - value shared by *all* instances
of a class. It is 1 value **per class**, instead of 1 value **per
instance**.

```java
class Duck{
    //static variable is initialised ONLY when class is first loaded
  //NOT EACH TIME A NEW INSTANCE IS MADE
  // btw no need to =0 cuz default is 0
    private static int duckCount=0;
    public Duck(){
        //now this works cuz duckCount is static and won't be reset to 0
        duckCount++;
    }
    //rmb to access static variable with class name
    System.out.println(Duck.duckCount);
}
```

<img src="/assets/images/posts/java/Static/2_static.png" title="제목" alt="아무거나" width="400"/>

>Static variables are shared.
All instances of the same class share a single copy of the static variables.

> instance variables: 1 per instance

> static variables: 1 per class

## 2 ways of static initalisation
>Static variables in a class are initialized before *any object* of that class
can be created.

> Static variables in a class are initialized before *any static method* of the
class runs.

### 1) static + final
A variable marked *final* means that—once initialized—it can never
change. In other words, the value of the static final variable will stay the
same as long as the class is loaded. Look up Math.PI in the API, and you’ll
find:

```java
public static final double PI = 3.141592653589793;
```

### 2) static initialiser
I saw this done in Spring Boot but didn't understand. Let's see.

>A static initializer is a block of code that runs when a class is loaded,
before any other code can use the class, so it’s a great place to
initialize a static final variable.

```java
class ConstantInit1 {
  final static final double X;
  
  static {
    X = Math.random();
  }
}
```

## Handy example
What would compiler print for this example?
```java
class StaticSuper {
    static {
        System.out.println("super static block");
    }
    
    StaticSuper () {
        System.out.println("super constructor");
    }
    
    }
    public class StaticTests extends StaticSuper {
        static int rand;
        
        static {
          rand = (int) (Math.random() * 6);
          System.out.println("static block " + rand);
        }
        
        StaticTests() {
            System.out.println("constructor");
        }
        
        public static void main(String[] args) {
            System.out.println("in main");
            StaticTests st = new StaticTests();
    }
}
```

Compiler prints:
```java
//super static block
//static block 3
//in main
//super constructor
//constructor
```
Notice that as the output below demonstrates, the static blocks for both classes run before
either of the constructors run.
