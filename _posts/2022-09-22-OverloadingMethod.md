---
date: 2022-09-22 14:35:23
layout: post
title: Overloading method
subtitle: Java
category: Java
tags:
  - Java

  
---

## Overloading method

There is no polymorphism involved here. Overloading means having 2 methods with same
name but different argument list.

Overloading lets you make multiple versions of a method, with different
argument lists, for convenience to the callers. For example, if you have a
method that takes only an int, the calling code has to convert, say, a double
into an int before calling your method. But if you overloaded the method with
another version that takes a double, then you’ve made things easier for the
caller.

```java
public class Overloads {
    String uniqueID;
    public int addNums(int a, int b) {
        return a + b;
    }
    public double addNums(double a, double b) {
        return a + b;
    }
    public void setUniqueID(String theID) {
        // lots of validation code, and then:
        uniqueID = theID;
    }
    public void setUniqueID(int ssNumber) {
        String numString = "" + ssNumber;
        setUniqueID(numString);
    }
}
```

1) return types can be different
2) but you can't change ONLY the return type


   If only the return type is different, it’s not a valid overload—the
   compiler will assume you’re trying to override the method. And even
   that won’t be legal unless the return type is a subtype of the return type
   declared in the superclass. To overload a method, you MUST change
   the **argument list**, although you can change the return type to anything.

3) You can vary the access levels in any direction.

You’re free to overload a method with a method that’s more restrictive.
It doesn’t matter, since the new method isn’t obligated to fulfill the
contract of the overloaded method.

