---
layout: post
title: OracleDatabaseException table or view does not exist error when generate-ddl is set to none 
category: Querydsl 
tags:
  - Querydsl
  
---
## Issue
I was mismatching entity’s table name (@Table(name = “IAR_LOG”)) with the 
DB’s table name which is IAR_SERVICE_LOG.

So I was making a query using querydsl like
```java
queryFactory.select(Projections.fields(IarLogsWithPartnerDto.class,
    iarLogs.id,
    iarLogs.createdAt))
    .from(iarLogs)
    .fetch();
```

This querydsl function gave me 
`OracleDatabaseException: table or view does not exist` error and I checked 
everywhere, like tableInterceptor to see how the sql is mapped and 
specifically, how the table NAME is altered through the interceptor. 
But the interceptor did nothing it just passed the table name as

```oracle
iarlogs0_.id
iarlogs0_.created_at
from
iar_log iarlogs0
```

I cross-checked with another log function and this is when I should have 
realised that THAT log function did a sql query that took table name like 
this:

```oracle
from
idrs_service_log idrslogs0_
```

Notice the difference? Idrs_service_log VS Iar_log?

## Solution
Basically Iar_log table does not exist in the DB, Iar_service_log table is the one that exists. Since generate-ddl setting was set to none and not create or update that executes the DDL that updates existing or create an entirely new one, we have to adjust to the existing table in DB.

A note on querydsl is that the Qclass that we place in from() is made via = new QIarLogs(“iarlogs”) constructor. 

