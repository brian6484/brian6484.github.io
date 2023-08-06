---
layout: post
title: SQL Trigger and a possible error
category: Database
tags:
  - Database
---
## Issue and solution
When i select some fields from my log table, it worked perfectly fine
But when i selected those fields from my log table and try inserting into 
a new stat table, i came across stat id null error.

Its not that you need id of the log table. The target table (stat) should 
have an auto-incrementing primary key or else you need to explicitly 
select or generate each id for each row being inserted.

Like
```sql
Insert into
Values (seq_stats.NEXTVAL, “0”, 123)
```

But this way only increment pk once. If you are selecting multiple rows, 
it will stop after 1 row.

So you need to somehow have an auto-incrementing system to increment pk 
of target table - a **sql trigger**.

## What is sql trigger?
tbc

## Resetting sql trigger
you may not have permission to drop and create sequence if you see that the current value of sequence is messed up and want to reset

`SELECT SEQ_IAR_STATS.NEXTVAL FROM DUAL;`

If nextval is something like 256, you have to take 1 value less than that which is 255 and

`ALTER SEQUENCE SEQ_IAR_STATS INCREMENT BY -235;`

Check if it has been reset by doing the first command again

`SELECT SEQ_IAR_STATS.NEXTVAL FROM DUAL;`

Finally do

`ALTER SEQUENCE SEQ_IAR_STATS INCREMENT BY 1;`

