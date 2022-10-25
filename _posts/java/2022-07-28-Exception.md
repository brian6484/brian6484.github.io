---
layout: post
title: Java's Exception handling
subtitle: Java 
description: Java
category: Java
tags:
  - Java
  - Head First Java

## Intro
So, how does a method tell you it might throw an exception? You find a
**throws** clause in the risky method’s declaration.

> Risky methods that could fail at runtime declare the exceptions that might happen using
“throws SomeKindOfException” on their method declaration.

## Try-catch to catch the exception
<img src="/assets/images/posts/java/Exception/exception1.png" title="제목" alt="아무거나" width="400"/>

Basically, I am gonna **TRY** this risky thing, and I will
**CATCH** myself if it fails.

A try/catch block tells the compiler that you know an exceptional thing could
happen in the method you’re calling, and that you’re prepared to handle it.
That compiler doesn’t care how you handle it; it cares only that you say
you’re taking care of it.

## Exception is an **object** of type Exception
Everything in Java is an object remember? Even exceptions.

Remember polymorphism's property so
an object of type Exception can be an instance of any **subclass** of Exception.

<img src="/assets/images/posts/java/Exception/exception3.png" title="제목" alt="아무거나" width="400"/>

Because an Exception is an object, what you catch is an object. In the
following code, the catch argument is declared as type Exception, and the
parameter reference variable is e.

<img src="/assets/images/posts/java/Exception/exception2.png" title="제목" alt="아무거나" width="400"/>

## If it’s your code that catches the exception, then whose code throws it?

You’ll spend much more of your Java time handling exceptions than
creating and throwing them yourself. For now, just know that
when your code calls a risky method —a method that declares an exception—
it’s the risky method that throws the exception back to you, the caller.

In reality, it might be you who wrote both classes. It really doesn’t matter
who writes the code...what matters is knowing which method throws the
exception and which method catches it.

When somebody writes code that could throw an exception, they must
declare the exception too!

<img src="/assets/images/posts/java/Exception/exception4.png" title="제목" alt="아무거나" width="400"/>

>One method will catch what another method throws. An exception is
always thrown back to the caller.
> 
> The method that throws has to declare that it might throw the exception.

1) If you throw an exception in your code, you must declare it using the
throws keyword in your method declaration.

2) If you call a method that throws an exception (in other words, a
method that declares it throws an exception), you must acknowledge
that you’re aware of the exception possibility. One way to satisfy the
compiler is to wrap the call in a try/catch. (There’s a second way we’ll
look at a little later in this chapter.)

## Runtime exception
Exceptions that are NOT subclass of RuntimeException are checked by 
compiler (i.e. "checked exceptions"). But RuntimeException are
not checked by compiler (i.e. "unchecked exceptions). You can do
throw catch and declare RuntimeException but you don't have to cuz
the ocmpiler doesn't check anyway. **Any exception class that extends
RuntimeException gets a free pass.**

Subclasses of RuntimException are ClassCastException and NullPointerException.

The compiler does not check cuz most RuntimeExceptions come from a problem in your code logic,
rather than a condition that fails at runtime in ways that you cannot
predict or prevent. A try/catch is for handling exceptional situations, not flaws in your code.
So it is not appropriate here.

## 2 or multiple exception handling
```java
public class Laundry{
    public void doLaundry() throws PantsException, LingerieException{
        //code that can throw either exception
    }
}
```

Then, to invoke this risky method with try & catch:
```java
public class WashingMachine{
    public void go(){
        Laundry laundry = new Laundry();
        try{
            laundry.doLaundry();
        } catch(PantsException pex){
          //recovery code
        } catch(LingerieException lex){
            //recovery code
        }
    }
}
```

### multiple catch blocks MUST be ordered from small to big
<img src="/assets/images/posts/java/Exception/exception6.png" title="제목" alt="아무거나" width="400"/>

The higher up the inheritance tree, the bigger the catch “basket.” As you
move down the inheritance tree, toward more and more specialized
Exception classes, the catch “basket” is smaller.

Looking at this diagram, ShirtException is big enuff to take
TShirtException or DressShirtException. But ClothingException is even
bigger (i.e. more things can be referenced using this exception type).
Then we have the mother of all catch arguments - **Exception**,
which can catch any exception.

So size matters when you have multiple catch blocks. The one with
the biggest basket has to be on the bottom. Or else, ones with smaller
baskets are useless because once the big basket catch block is executed,
the small basket catch, which is more specialised for
that particular exception, is overlooked.

Siblings (exceptions at the same level of the hierarchy tree)
can be in any order.

## Exceptions are polymorphic
Like all objects, exceptions can be referred polymorphically.
For example, a LingerieException *object* can be assigned to
a ClothingException *reference*.

<img src="/assets/images/posts/java/Exception/exception5.png" title="제목" alt="아무거나" width="400"/>

Advantage is that method does not have to explicitly declare
every possible exception it might throw - can just declare a superclass
of exceptions. 

Same with catch blocks - no need to write catch for each possible 
exception as long as your catch can handle any exception that is thrown.

1) can declare exceptions using a **superclass** of the exceptions you throw
```java
public void do Laundry() throws ClothingException{
    
  }
```
Declaring superclass (ClothingException) lets us throw any subclass
of this superclass like PantsException,LingerieException, etc without
explicitly declaring them **individually**.

2) can catch exception using a **superclass** of exception thrown
```java
  try{
      laundry.doLaundry();
  } catch(ClothingException cex){
    //recovery code
  } 
```

Using catch exception with superclass (ClothingException) can catch 
any ClothingException **subclass** like LingerieException and PantsException.

But good practice is to write a different catch block for each exception that you need to handle
uniquely.

