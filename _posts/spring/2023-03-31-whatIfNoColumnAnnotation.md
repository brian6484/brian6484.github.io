---
layout: post
title: What if we don't add @Column annotation to our fields? How are they mapped then?
category: Spring 
tags:
  - Spring

  
---
## No @Column
Automatically @Column properties are applied but it is applied
differently to Java primitive types where it blocks entering null 
values to primitive types

Actually this goes back to the basics of Java where primitive types like
int cannot hold value of null whereas reference or object wrapper class
can hold null values.

E.g.
int data1 //no @Column, primitive type
Data1 integer not null //created DDL

Integer data2 //no @Column, reference type
Data2 integer //created DDL

@Column
int data3 //now there is @Column for primitive
Data3 integer

For primitive like data1, you cannot enter null. But for reference data type
like data2, null is allowed. When there is @Column for primitive, the 
default is (nullable=true) so it does not places NOT NULL condition on 
a primitive. So if you want to use @Column on primitive, put 
@Column(nullable=false).

This concept is well-explained by GTP sensei
>In Java, primitive types are not objects, they are simple data types. They are predefined by the language and do not have any methods or properties like objects. Because of this, primitive types do not have a concept of a "null" value, which is typically used to represent the absence of an object or the lack of a value.

>In Java, the value of a primitive type is always a valid value, even if it is zero or false. This is why you cannot assign a null value to a variable of a primitive type. If you need to represent the absence of a value for a primitive type, you can use a special value, such as -1 for integers or false for booleans, depending on the context.
However, if you need to work with values that may be null, you can use their corresponding object wrapper classes. For example, instead of using an int, you can use an Integer object, which can be assigned a null value.



