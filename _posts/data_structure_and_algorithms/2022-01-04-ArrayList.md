---
date: 2022-01-04 14:35:23
layout: post
title: ArrayList
subtitle: 
description:
category: Data structure & Algorithms
tags:
  - Data structure & Algorithms
  - Head First Java
---
# ArrayList in Java:

Unlike the regular array, ArrayList is more flexible in that initial size need not be declared and that it can shrink when elements are removed. (dynamic)
Also, instead of looping through the whole array, you can ask if it contains the element you are looking for. But array is faster than arraylist when it comes
to *primitives* because arraylist needs to do wrapping and unwrapping.

Head First Java states 3 characteristics about ArrayList:
* An ArrayList resizes dynamically to whatever size is needed. It
  grows when objects are added, and it shrinks when objects are
  removed.

* Although an ArrayList holds objects and not primitives, the
compiler will automatically “wrap” (and “unwrap” when you take
it out) a primitive into an Object and place that object in the
ArrayList instead of the primitive.

* You declare the type of the array using a type parameter (<>), which is
  a type name in angle brackets. Example: ArrayList<Dog> means
  the ArrayList will be able to hold only objects of type Dog (or
  subclasses of Dog)

Also, arrays don't have methods except its instance variable - length but arraylists do. 

## ArrayList methods

1) add(E e) - appends specified element to the END of the list
2) remove(int index) - removes element at specified index 
3) remove (Object o) - removes first occurrence of specified element (okay technically, it was not removing the object from array but
making a copy of the *reference* to that object and setting it to *null* or another object variable. But arrayList can actually remove 
its reference entirely)
4) contains (Object o) - boolean that returns true if it has that specified element
5) isEmpty() - boolean that returns true if it is empty
6) indexOf(Object o ) -  returns either the first index of that element or -1 if not found
7) size() - returns number of elements in the list
8) get(int index) - returns element at specified position









