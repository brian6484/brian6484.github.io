---
layout: post
title: Java nested class
subtitle: Java 
description: Java
category: Java
tags:
  - Java
  - Head First Java
---
## Intro
[This reference](https://docs.oracle.com/javase/tutorial/java/javaOO/nested.html)
describes well about nested classes and its 2 types - non-static and
static.

>  Non-static nested classes are called inner classes. Nested classes that are declared static are called static nested classes.

```java
class Outerclass{
    class InnerClass{
        
    }
    static class StaticNestedClass{
        
  }
}
```

A nested class is a member of its enclosing class (OuterClass).
Inner classes have access to other members of the enclosing class,
even if they are declared private. Static nested class, on the other
hand, cannot access other members of the enclosing class.

## Why nested class?
1) We can logically group classes that are going to be only used in
one place.

If a class is useful to only one other class, then it is logical to embed it in that class and keep the two together. Nesting such "helper classes" makes their package more streamlined.

2) It increases encapsulation

```java
class Hola{
    //members in this Hola class
}
class Hello{
    
}
```

If we have such 2 top-level classes Hola and Hello and Hello needs
access to members of A, the members cannot be declared private
and must be public.

But by hiding class Hello **within** Hola, Hola's members can be
declared private and Hello can access them. Furthermore, Hello itself
can be hidden and *encapsulated* from the outside world.

3) can lead to more readable and maintainable code

Nesting small classes within top-level class *places* the code
closer to where it is used.

## Inner class
```java
class Ourerclass{
    class Innerclass{
        
    }
}
```

First, let's recall the difference between **instance method** and
**static method**. Instance method requires an object of its class
to be created first, before it can be invoked. Static method, like
static methods from Math, do not require creation of objects and
can just be invoked.

Coming back to inner class, it is associated with an instance of its 
enclosing class so it has direct access to that object's methods and
fields. It can also access instance methods and variables.
Also, since it is associated with an instance, it
**cannot define any static members itself**.

An instance of InnerClass can exist only within an instance of OuterClass and has direct access to the methods and fields of its enclosing instance.

To instantiate an inner class, you first must instantiate the
outer class. Then, create the inner object **within** the outer object
with this syntax

```java
Outerclass outerobject = new Outerclass();
Outerclass.Innerclass innerobject = outerobject.new Innerclass();
```

## Static nested class
Static nested class, like static class methods, cannot refer 
directly to instance variables or methods like nested class.
However, it can access them **only through** object reference
like this.

First you instantiate a static nested class, the same way
as a top-level class.

```java
StaticNestedClass staticNestedObject = new StaticNestedClass();
```

For example,
```java
public class OuterClass {

    String outerField = "Outer field";
    static String staticOuterField = "Static outer field";

    class InnerClass {
        void accessMembers() {
            System.out.println(outerField);
            System.out.println(staticOuterField);
        }
    }

    static class StaticNestedClass {
        void accessMembers(OuterClass outer) {
            // Compiler error: Cannot make a direct static reference to the 
          // non-static field outerField, can only do through obj reference
            // System.out.println(outerField);
            System.out.println(outer.outerField);
            System.out.println(staticOuterField);
        }
    }

    public static void main(String[] args) {
        System.out.println("Inner class:");
        System.out.println("------------");
        OuterClass outerObject = new OuterClass();
        OuterClass.InnerClass innerObject = outerObject.new InnerClass();
        innerObject.accessMembers();

        System.out.println("\nStatic nested class:");
        System.out.println("--------------------");
        StaticNestedClass staticNestedObject = new StaticNestedClass();        
        staticNestedObject.accessMembers(outerObject);
        
        System.out.println("\nTop-level class:");
        System.out.println("--------------------");
        TopLevelClass topLevelObject = new TopLevelClass();        
        topLevelObject.accessMembers(outerObject);                
    }
}

public class TopLevelClass {

  void accessMembers(OuterClass outer) {
    // Compiler error: Cannot make a static reference to the non-static
    //     field OuterClass.outerField
    // System.out.println(OuterClass.outerField);
    System.out.println(outer.outerField);
    System.out.println(OuterClass.staticOuterField);
  }
}
```

The output is as such:
```java
Inner class:
------------
Outer field
Static outer field

Static nested class:
--------------------
Outer field
Static outer field

Top-level class:
--------------------
Outer field
Static outer field
```

Static nested class can indeed interact with instance members
of its our class like any top-level class, **through object reference**.
The static nested class StaticNestedClass can't directly access outerField because it's an instance variable of the enclosing class, OuterClass.
Only through obj reference like outer.outerField.

Similarly, the top-level class TopLevelClass can't directly access outerField either.

