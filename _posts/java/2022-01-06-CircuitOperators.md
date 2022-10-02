---
date: 2022-01-06 14:35:23
layout: post
title: Short-Circuit Operators ( && , || ) vs Non-Short-Circuit Operators ( &, | )
description:
category: Java
tags:
  - Java
  - Head First Java
---
## Short-Circuit Operators ( && , || ):

In the case of &&, the expression will be true **only if both** sides of
the && are true. So if the JVM sees that the left side of a && expression is
false, it stops right there! Doesn’t even bother to look at the right side. Same for ||.

If there is an expression with &&(logical AND), and the first operand itself is false, then a short circuit occurs, the further expression is not evaluated, and false is returned.

Use case is that if we don't know if this reference variable has been assigned to an object,
if we call this null reference variable, we get *NullPointerException*. So try

```java
if (refVar != null && refVar.isValidType()) {
  // do ‘got a valid type’ stuff
}
```

## Long-Circuit Operators(& , | )
When used in boolean expressions, the & and | operators act like their &&
and || counterparts, except that they force the JVM to **always** check **both** sides
of the expression. So even when left side is false, it still checks the right side.
Typically, & and | are used in another context, for manipulating bits.












