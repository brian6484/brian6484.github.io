---
date: 2022-06-09 14:35:23
layout: post
title: Comparable, Comparator generics and Intro to Lambda
subtitle: Java 
description: Java
category: Java
tags:
  - Java
  - Head First Java
---

## Intro
Let's say we want to sort a list of Song objects using Collections.sort() method.
It definitely works for list of Strings but will it work for Song objects? NO!

<img src="/assets/images/posts/java/Generics/3_generics.png" title="제목" alt="아무거나" width="400"/>

The sort method only takes list of *Comparable* objects. Song is not a subtype of Comparable
so you cannot sort it. Not yet...


## A note on T extends Comparable
A note is that String does not **Extend** comparable. It implements it. 

```java
public final class String
implements java.io.Serializable, Comparable<String>,
CharSequence {

```

> Comparable is an interface. Why does it say <T extends Comparable> if Comparable is an
interface? Shouldn't it be implements?

**In generics, extends mean both extends OR implements.**

The Java engineers had to give you a way to put a constraint on a
parameterized type so that you can restrict it to, say, only subclasses of
Animal. But you also need to constrain a type to allow only classes that
implement a particular interface. So here’s a situation where we need one
kind of syntax to work for both situations—inheritance and implementation.
In other words, that works for both extends and implements.

And the winning word was...extends. But it really means “IS-A” and works
regardless of whether the type on the right is an interface or a class.

## Comparable sort()
We can pass the ArrayList<Song> to the sort() method **only if** the Song class
implements Comparable.

```java
public interface Comparable<T>{
    int compareTo(T o);
}
```
compareTo returns some integer if this object is *greater* or *less than* a specified
object. But how do you determine this size? Which song is greater or less? How do you
determine this? Until you do this, you cannot implement this interface.

We can compare by title of song for example.

<img src="/assets/images/posts/java/Generics/4_generics.png" title="제목" alt="아무거나" width="400"/>

##sort() method on Collections that takes a Comparator
The previous solution with **Comparable element** worked only for comparing via 1 field. What if we want to 
sort via title and artist? Use a custom **Comparator**!

A **Comparable element** in a list can compare itself to another of its own type
in **only one way**, using its compareTo() method. But a **Comparator** is
external to the element type you’re comparing—it’s a separate class. So you
can make as many of these as you like! Want to compare songs by artist?
Make an ArtistComparator. Sort by beats per minute? Make a
BpmComparator.

```java
public interface Comparator<T>{
    int compare (T o1, T o2);
}
```

<img src="/assets/images/posts/java/Generics/5_generics.png" title="제목" alt="아무거나" width="400"/>

As you see, a lot of repetitive code goes into this. A solution is inner class/
argument-defined anonymous inner class.

```java
songList.sort(new Comparator<SongV3>() {
public int compare(SongV3 one, SongV3 two) {
    return one.getTitle().compareTo(two.getTitle());
}
});
```

But still, there is a lot of code for just wanting to sort by title. 

Solution: Lambda!!!


## Differentiating comparable and comparator
Invoking the Collections.sort(List list) method means the list
element’s compareTo() method determines the order. The elements in
the list MUST implement the Comparable interface.

Invoking List.sort(Comparator c) or Collections.sort(List list,
Comparator c) means the Comparator’s compare() method will be
used. That means the elements in the list do NOT need to implement the
Comparable interface, but if they do, the list element’s compareTo()
method will NOT be called.

> If you pass a Comparator to the sort() method, the sort order is determined by the
Comparator.
> 
> If you don’t pass a Comparator and the element is Comparable, the sort order is
determined by the element’s compareTo() method.

