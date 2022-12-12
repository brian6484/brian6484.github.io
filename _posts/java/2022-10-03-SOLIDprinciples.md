---
layout: post
title: SOLID principles of object-oriented design
category: Java
tags:
  - Java
---
## Reason for SOLID principles
> Design principles encourage us to create more maintainable, 
understandable and flexible software. Consequently, as our application
grows in size, we can reduce their complexity (and saves us from headaches
down the road!)

The 5 concepts are:
1) Single Responsibility
2) Open/Closed
3) Liskov Substitution
4) Interface Segregation
5) Dependency Inversion

## Single Responsibility
Class should only have **one responsibility**. Furthermore, it should only
have 1 reason to change. 

Example:
```java
public class Book {

    private String name;
    private String author;
    private String text;

    //constructor, getters and setters

    // methods that directly relate to the book properties
    public String replaceWordInText(String word, String replacementWord){
        return text.replaceAll(word, replacementWord);
    }

    public boolean isWordInText(String word){
        return text.contains(word);
    }
}
```

However, when we want to add a method to print the book's content:
```java
    void printTextToConsole(){
        // our code for formatting and printing the text
    }
```

This violates the single responsibility principle. To resolve this,
we should implement a separate class that deals only with printing our texts:
```java
public class BookPrinter {

    // methods for outputting text
    void printTextToConsole(String text){
        //our code for formatting and printing the text
    }

    void printTextToAnotherMedium(String text){
        // code for writing to any other location..
    }
}
```

Not only have we developed a class that relieves the Book of its printing duties, but we can also leverage our BookPrinter class to send our text to other media.

### Advantages
1) Testing – A class with one responsibility will have far fewer test cases.
2) Lower coupling – Less functionality in a single class will have fewer dependencies.
3) Organization – Smaller, well-organized classes are easier to search than monolithic ones.

## Open for extension, Closed for modification
classes should be open for extension but closed for modification. In doing so, we stop ourselves from modifying existing code and causing potential new bugs in an otherwise happy application.
Of course, the **one exception to the rule** is when fixing bugs in existing code.

For example, we have a Guitar class with attributes like model and volume.
Now what if we decide the Guitar is a little boring and could use a cool flame pattern to make it look more rock and roll?

We can be tempted to just directly open up and modify the Guitar class
and add a flame pattern. But we are gonna violate this principle that
it should be closed for modification (plus possible errors in existing
code that utilises this Guitar class)

So, let's stick to the open-closed principle and simply **extend our Guitar class**:
```java
public class SuperCoolGuitarWithFlames extends Guitar {

    private String flameColor;

    //constructor, getters + setters
}
```

By extending the Guitar class, we can be sure that our existing application won't be affected.

## Liskov Substitution
>  if class A is a subtype of class B, we should be able to replace B with A without disrupting the behavior of our program.

Oh wait, I mixed up subtype with subclass. So my analogy below is
wrong: (pls ignore)
So for example, if Dog (A) is a subtype of Animal (B), we should 
be able to replace Animal (B) with Dog (A) without problem.

> Subclasses allow one to reuse the code inside classes - both instance variable declarations and method definitions. Thus they are useful in supporting code reuse inside a class. Subtyping on the other hand is useful in supporting reuse externally, giving rise to a form of polymorphism. That is, once a data type is determined to be a subtype of another, any function or procedure that could be applied to elements of the supertype can also be applied to elements of the subtype.

The correct example:
```java
public interface Car {

    void turnOnEngine();
    void accelerate();
}


public class MotorCar implements Car {

  private Engine engine;

  //Constructors, getters + setters

  public void turnOnEngine() {
    //turn on the engine!
    engine.on();
  }

  public void accelerate() {
    //move forward!
    engine.powerOn(1000);
  }
}
```

So with Liskov Substitution, technically we can replace Car with
MotorCar.

But what if we add ElectricCar with no turnOnEngine method and
a different form of acceleration method?
```java
public class ElectricCar implements Car {

    public void turnOnEngine() {
        throw new AssertionError("I don't have an engine!");
    }

    public void accelerate() {
        //this acceleration is crazy!
    }
}
```

By throwing a car without an engine into the mix, we are inherently changing the behavior of our program. This is a blatant violation of Liskov substitution and is a bit harder to fix than our previous two principles.

One possible solution would be to rework our model into interfaces that take into account the engine-less state of our Car.


## Interface Segregation
Larger interfaces should be split into smaller ones. By doing so, we can ensure that implementing classes only need to be concerned about the methods that are of interest to them.

For example, this large interface:
```java
public interface BearKeeper {
    void washTheBear();
    void feedTheBear();
    void petTheBear();
}
```

As avid zookeepers, we're more than happy to wash and feed our beloved bears. But we're all too aware of the dangers of petting them. Unfortunately, our interface is rather large, and we have no choice but to implement the code to pet the bear.

Let's fix this by splitting our large interface into three separate ones:

```java
public interface BearCleaner {
    void washTheBear();
}

public interface BearFeeder {
    void feedTheBear();
}

public interface BearPetter {
    void petTheBear();
}
```

Now, thanks to interface segregation, we're free to implement only the methods that matter to us:
```java
public class BearCarer implements BearCleaner, BearFeeder {

    public void washTheBear() {
        //I think we missed a spot...
    }

    public void feedTheBear() {
        //Tuna Tuesdays...
    }
}

public class CrazyPerson implements BearPetter {

  public void petTheBear() {
    //Good luck with that!
  }
}
```

Going further, we could even split our BookPrinter class from our example earlier to use interface segregation in the same way. By implementing a Printer interface with a single print method, we could instantiate separate ConsoleBookPrinter and OtherMediaBookPrinter classes.

## Dependency Inversion
This refers to decoupling of software modules. Instead of 
high-level modules depending on low-level modules, both will depend
on abstractions.

For example, add attributes of monitor and keyboard to our computer's
constructor so that any computer we instantiate comes with those
attributes:

```java
public class Windows98Machine {

    private final StandardKeyboard keyboard;
    private final Monitor monitor;

    public Windows98Machine() {
        monitor = new Monitor();
        keyboard = new StandardKeyboard();
    }

}
```

Problem is, **By declaring the StandardKeyboard and Monitor with the new keyword, we've tightly coupled these three classes together.**

Not only does this make our Windows98Computer hard to test, but we've also lost the ability to switch out our StandardKeyboard class with a different one should the need arise. And we're stuck with our Monitor class too.

Let's decouple our machine from the StandardKeyboard by adding a more general Keyboard interface and using this in our class:

```java
public interface Keyboard {
    
}

public class Windows98Machine{

    private final Keyboard keyboard;
    private final Monitor monitor;

    public Windows98Machine(Keyboard keyboard, Monitor monitor) {
        this.keyboard = keyboard;
        this.monitor = monitor;
    }
}
```

This is dependency injection pattern to help add the Keyboard dependency
to our computer class. 

Let's also modify our StandardKeyboard class to implement the Keyboard interface so that it's suitable for injecting into the Windows98Machine class:
```java
public class StandardKeyboard implements Keyboard { }
```

Now our classes are decoupled and communicate through the Keyboard abstraction. If we want, we can easily switch out the type of keyboard in our machine with a different implementation of the interface. We can follow the same principle for the Monitor class.

