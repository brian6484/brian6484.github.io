---
layout: post
title: Setting up H2 database 
category: Database
tags:
  - Database
---
## What is SQL trunc?
Whilst it has many usages, SQL trunc can be used to truncate(delete) part 
of your date/timestamp to a specified level of precision. For my case, my 
localdatetime was too precise to the point of milliseconds, while I needed 
just the date precision so I did 

```sql
TRUNC(log.CREATED_AT)
```
