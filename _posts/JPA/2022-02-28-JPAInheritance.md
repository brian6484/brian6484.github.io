---
date: 2022-02-28 14:35:23
layout: post
title: Java inheritance in JPA
description: 
category: JPA
tags:
  - JPA
---

## Java inheritance
We have looked at [Java inheritance](https://brian6484.github.io/java/2022/01/21/Inheritance.html)
but let's look at how it is applied to JPA

good reference: https://www.baeldung.com/hibernate-inheritance

## Inheritance in JPA
There are multiple strategies to choose from

### Single table strategy
The Single Table strategy creates one table for each class hierarchy. JPA also chooses this strategy by default if we don't specify one explicitly.

```java
@Entity
@Inheritance(strategy = InheritanceType.SINGLE_TABLE)
public class MyProduct {
    @Id
    private long productId;
    private String name;

    // constructor, getters, setters
}
```

Note that the The **identifier (id)** of the entities is also defined in the superclass.

Then for the subclasses, 
```java
@Entity
public class Book extends MyProduct {
    private String author;
}
```

```java
@Entity
public class Pen extends MyProduct {
    private String color;
}
```

We also need discriminator values because the records for all entities will be in the same table, Hibernate needs a way to differentiate between them.
By default, this is done through a discriminator column called **DTYPE** that has the name of the entity as a value.

To customize the discriminator column, we can use the @DiscriminatorColumn annotation:

```java
@Entity(name="products")
@Inheritance(strategy = InheritanceType.SINGLE_TABLE)
@DiscriminatorColumn(name="product_type", 
  discriminatorType = DiscriminatorType.STRING)
public class MyProduct {
    // ...
}
```

```java
@Entity
@DiscriminatorValue("book")
public class Book extends MyProduct {
    // ...
}
```

If @DiscriminatorValue is not explicitly set in the subclass,
the class name of subclass is taken as the value by default.
