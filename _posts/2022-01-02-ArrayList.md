---
date: 2022-01-02 14:35:23
layout: post
title: ArrayList
description:
category: Java
tags:
  - Java
  
* ArrayList in Java:

Unlike the regular array, ArrayList is more flexible in that initial size need not be declared and that it can shrink when elements are removed. (dynamic)
Also, instead of looping through the whole array, you can ask if it contains the element you are looking for. But array is faster than arraylist when it comes
to primitives because arraylist needs to do wrapping and unwrapping.

Basically arrays don't have methods except its instance variable length but arraylists do. Here are the following: 

1) add(E e) - appends specified element to the END of the list
2) remove(int index) - removes element at specified index 
3) remove (Object o ) - removes first occurrence of specified element (okay technically, it was not removing the object from array but
making a copy of the *reference* to that object and setting it to *null* or another object variable. But arrayList can actually remove 
its reference entirely)
4) contains (Object o) - boolean that returns true if it has that specified element
5) isEmpty() - boolean that returns true if it is empty
6) indexOf(Object o ) -  returns either the first index of that element or -1 if not found
7) size() - returns number of elements in the list
8) get(int index) - returns element at specified position









