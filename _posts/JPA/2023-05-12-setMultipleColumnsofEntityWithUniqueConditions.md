---
layout: post
title: @UniqueConstraints and for multiple column conditions(제약조건) where @Column is insufficient
category: JPA
tags:
  - JPA
---
  
## Issue
```java
@Table(
   uniqueConstraints={
		@UniqueConstraint( columnNames={"column1"})
   }
)


      


@Table(
   uniqueConstraints = {
  	@UniqueConstraint(name = "UniqueNumberAndStatus", columnNames = {"personNumber", "isActive"}),
  	@UniqueConstraint(name = "UniqueSecurityAndDepartment", columnNames = {"securityNumber", "departmentCode"})
  }

```

Difference between @Column(unique=true) and this table uniqueConstraints is that uniqueConstraints can work on a SET of columns (e.g. {col1,col2}). unique=true is for only 1 column but if you want to set 2 or more columns use uniqueConstraints

They both set unique conditions for columns BUT
If you are not using DDL to create tables (e.g. ddl-auto = create) and instead, using your own DDL or tools to make your own tables and DB, they dont work!

Because they work only when DDL is automatically generated (create) and they have no effect on the logic of JPA
