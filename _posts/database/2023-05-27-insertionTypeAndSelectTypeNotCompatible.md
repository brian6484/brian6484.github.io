---
layout: post
title: Solve insertion type and select type at position 9 are not compatible error
category: Database
tags:
  - Database
---
## Issue and solution
This only applies when you are trying to **use native sql instead of querydsl** and
forcing fields into a pure sql query. The types of entity's fields need to be
considered whether they match the constraints of the DB you are using.

The field type that I was trying to get and insert by performing outer joining does not seem to match with the field im trying to select. I double checked the column constraint but both were NUMBER (10,0).

Turns out the field in that table was Long while mine was Integer.

## If the error is not still fixed 
Even if you cast to an explicit type and still get this error, it is 
possible your database schema is the problem. For me, I declared my 
database column as NUMBER but my JPA entity is an Integer. Actually number 
also accepts Integer but im not sure why there was this error. So I 
deleted the table and created a fresh new table that accepts

“RELAY_SUCCESS_COUNT INTEGER”

I think it is probably cuz if you allowed JPA to create the database 
schema automatically and not put ddl as none, then this problem would 
not have occurred. But since I was using native SQL, this problem arised.
