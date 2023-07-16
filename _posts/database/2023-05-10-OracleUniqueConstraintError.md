---
layout: post
title: Unique constraint error in Oracle db
category: Database
tags:
  - Database
---
## Issue
I was making a test case and making an entity with id field of 1000L when 
I came across this issue. I checked the DB but 1000L was not used in DB, 
only up till 100L. Very strange, I tested with 1L which WAS in DB and 
Hibernate sent an update query, updating the column with id =1. That is 
strange cuz update was allowed but insert resulted in error.

## Approach
I asked my senior and we looked at the DB’s constraint and very 
importantly, the Sequences. I made the id generator to follow 
strategy.SEQUENCE via JPA. It looked normal, with min value =1, cant 
really rmb what value: field’s value was. 
Literally the value: (?what value was this).

## Solution
Anyway, we can check it via
SELECT SEQ_SERVICE_LOG_ID.CURRVAL FROM DUAL;

And it was 43. But wtf the db had logs filled till id =100. Turns out my senior filled out the logs forcefully without using the seq generator so there was a conflict. If I inputted id=43 or 44 it might have worked.

We tried INSERT INTO IAR_SERVICE_LOG (ID,CREATED_AT) VALUES (SEQ_SERVICE_LOG_ID.NEXTVAL, sysdate)

But exception still occurred

So factory reset was required (we tried changing via UI of DBeaver by going to sequence and typing 200 into value: field but didnt work)

```oracle
DROP SEQUENCE SEQ_SERVICE_LOG_ID

CREATE SEQUENCE IAR.SEQ_SERVICE_LOG_ID INCREMENT BY 1 MINVALUE 2021 MAXVALUE 9999999999999999999999999 NOCYCLE CACHE 20 NOORDER;
```

## Quiz if you get it
What if the sequence generator’s value is 220 and i deleted some 
records with ID less than 220? Will new records be filled with ID less
or greater than 220?

Actually it will be filled with ID less than 220.
