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

E.g.
Int data1 //no @Column, primitive
Data1 integer not null //created DDL

Integer data2 //no @Column, reference
Data2 integer //created DDL

@Column
Int data3 //now there is @Column for primitive
Data3 integer

For primitive like data1, you cannot enter null. But for reference data type
like data2, null is allowed. When there is @Column for primitive, the 
default is (nullable=true) so it does not places NOT NULL condition on 
a primitive. So if you want to use @Column on primitive, put 
@Column(nullable=false).


