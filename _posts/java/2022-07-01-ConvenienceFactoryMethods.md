---
layout: post
title: Java's Convenience factory methods 
subtitle: Java 
description: Java
category: Java
tags:
  - Java
  - Head First Java
---

## Intro
Convenience Factory Methods for Collections allow you to easily create a
List, Set, or Map that’s been prefilled with known data. However,
there are 2 precautions

## Precautions
### The resulting collections cannot be changed
You can’t add to them
or alter the values; in fact, you can’t even do the sorting

### The resulting collections are not the standard Collections 
These are not ArrayList, HashSet, HashMap, etc. You can rely on
them to behave according to their interface: a List will always preserve
the order in which the elements were placed; a Set will never have
duplicates. But you can’t rely on them being a specific implementation
of List, Set, or Map.

## Methods
Convenience Factory Methods are just that—a convenience that will work
for most of the cases where you want to create a collection prefilled with
data. And for those cases where these factory methods don’t suit you, you can
still use the Collections constructors and add() or put() methods instead.

### List.of()
Create list of Strings
```java
List<String> strings = List.of("somersault", "cassidy",
"$10");
```

Create list of Objects
```java
List<SongV4> songs = List.of(new SongV4("somersault", "zero
7", 147),
new SongV4("cassidy", "grateful dead",
158),
new SongV4("$10", "hitchhiker", 140));
```

### Set.of()
```java
Set<Book> books = Set.of(new Book("How Cats Work"),
new Book("Remix your Body"),
new Book("Finding Emo"));
```

### Map.of(), for less than 10 entries
If you want to put less than 10 entries into your Map,
you can use Map.of, passing in key, value, key, value, etc

```java
Map<String, Integer> scores = Map.of("Kathy", 42,
"Bert", 343,
"Skyler", 420);
```

### Map.ofEntries, for more than 10 entries
We can be clearer about how the keys are paired up to their values
with this method

```java
Map<String, String> stores = Map.ofEntries(Map.entry("Riley","Supersports"),
                                            Map.entry("Brooklyn","Camera World"),
                                            Map.entry("Jay","Homecase"));
```
