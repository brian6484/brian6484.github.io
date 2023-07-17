---
layout: post
title: Different strategies of mapping PK (identity, sequence, automatic)
category: JPA
tags:
  - JPA
---
  
## Explained

Different ways of mapping PK:

직접할당: you set it urself

자동 생성: identity (key generation responsibility is to the db), sequence(uses db sequence to generate PK), table(creates a separate key generation table)

## 직접할당
직접할당:
```java
@Id @Column
private Long id
```

This strategy is where before you persist your entity via em.persist(), you allocate the PK urself to it

```java
Board board = new Board()
board.setId(1L)
em.persist(board)
```

## 자동생성
### automatic
Automatic:
Default @GeneratedValue is AUTO. This strategy actually chooses one of IDENTITY, SEQUENCE, TABLE strategies according to the DB. For example, if Oracle, chooses SEQUENCE, MySQL then it chooses IDENTITY.

### identity
Identity:
Allocates key generation responsibility to db (mysql, postgre, sql server)
For example, MySQL’s auto_increment generates and increments DB’s pk automatically. Unlike 직접할당, now when id column is empty, db puts the id value for us automatically

```java
Board board = new Board()
em.persist(board)
sout(board.getId())
//1
```

A note is that you have to persist the entity (save it) before you can get the PK value. This value is value that DB generated that JPA queried at the point when entity is persisted
Also, for entity to be in managed state, it needs PK. But IDENTITY needs to persist the entity in the DB before we can get the PK value. Thus, in this case, invoking em.persist() IMMEDIATELY delivers INSERT SQL to db

```sql
INSERT INTO BOARD (DATA) VALUES (1)
```


So this strategy **does not** for FetchType.LAZY

### sequence
Sequence:
For oracle, Postgre, H2, DB2

```java
@Entity
@SequenceGenerator(
	name = "USER_SEQ_GENERATOR"
    , sequenceName = "USER_SEQ"
    , initialValue = 1
    , allocationSize = 1
)
public class User {

    @Id
    @GeneratedValue(
    	strategy = GenerationType.SEQUENCE
    	, generator = "USER_SEQ_GENERATOR"
    )
    private long id;
    
}

Board board = new Board()
em.persist(board)
sout(board.getId())
//1

```

It is identical to IDENTITY, but the internal 동작 방식 is different. 
SEQUENCE is when you invoke em.persist(), it uses DB sequence first to 
search PK. Then, this queried PK is allocated to entity, THEN this 
entity is persisted. Then, transaction is committed and flush happens 
that sends all the stored SQL queries to DB, thus saving the entity 
to the DB.

This is different from IDENTITY, where it saves the entity to DB FIRST 
before searching PK and allocating that DB PK value to entity PK.

Btw allocationSize default is 50 to optimise performance.
https://dololak.tistory.com/479

