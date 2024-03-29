---
layout: post
title: Java Stream with Lambda
subtitle: Java 
description: Java
category: Java
tags:
  - Java
  - Head First Java
---
## Intro
Following on my [Stream post](https://brian6484.github.io/java/2022/07/04/Streams.html)
let's create some complex pipelines with Lambda.

## Stream + Lambda
We can customise the building blocks with Lambda

<img src="/assets/images/posts/java/Stream/stream4.png" title="제목" alt="아무거나" width="400"/>

## Example with filter()
Suppose we want to filter a list of Song objects by the genre
that contains the word "Rock" and output it as a List.

The filter method takes a **Predicate**.
<img src="/assets/images/posts/java/StreamLambda/streamlambda1.png" title="제목" alt="아무거나" width="400"/>

```java
List<Song> list = songs.stream()
  .filter(song -> song.getGenre().contains("Rock"))
  .collect(Collectors.toList());
```

## Example with map()
map() turns rectangles to circles. It states how to mape
*from* one type *to* another type.

Map method takes a **Function**. Function does 1 thing - it takes something
of one type and returns something of a different type.

<img src="/assets/images/posts/java/StreamLambda/StreamLambda2.png" title="제목" alt="아무거나" width="400"/>

The map’s lambda expression is similar to the one for filter; it takes a song
and turns it into something else. Instead of returning a boolean, it returns
some other object, in this case a String containing the song’s genre.

<img src="/assets/images/posts/java/StreamLambda/streamlambda3.png" title="제목" alt="아무거나" width="400"/>

Example:
```java
public int getTotalPrice(){
    int totalPrice=0;
    for (OrderItem orderItem: orderItems){
        totalPrice += orderItem.getTotalPrice();
    }
    return totalPrice;
}
```

Using Lambda:
```java
public int getTotalPrice(){
    int totalPrice= orderItems.stream().mapToInt(OrderItem::getTotalPrice).sum();
    return totalPrice;
}
```

## Example with distinct() VS .collect(Collectors.toSet())
Once you get the genres from Songs with map(), you may want unique
generes and not duplicates. Just add distinct() intermediary operation
to remove duplicates.

Advantage of using collect(Collectors.toSet()) is that anything that
uses that result *knows* it is a set by definition. But either is
fine.

## Collectors.joining
You can create a String result from the stream. It will join together all the
stream elements into a single String. You can optionally define the delimiter,
the character to use to separate each element. This can be very useful if you
want to turn your stream into a String of Comma Separated Values (CSV).








