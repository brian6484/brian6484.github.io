---
layout: post
title: JPA's Transactional and precautions
category: JPA
tags:
  - JPA
---
  
## Reference
https://mommoo.tistory.com/92

## Transaction
First of all, what is transaction?

Some 작업 needs to be executed without any error. But if an error
does occur in the middle of execution, transaction helps roll
back the changes right before the error occurred.

## What does transcational do
1) transaction begin, commit을 자동 수행해준다.
2) 예외를 발생시키면, rollback 처리를 자동 수행해준다.

## @Transactional's readOnly
When declared at class level, @Transactional(readOnly = true) applies to every method in that class. But we don't want to readOnly for saveItem, so we declare an exception to that method with @Transactional
```java
  @Service
  @Transactional(readOnly = true)
  @RequiredArgsConstructor
  public class ItemService {
      private final ItemRepository itemRepository;

      @Transactional //this makes it readOnly=false for this saveItem method
      // actually readOnly=false is default
      public void saveItem(Item item){
          itemRepository.save(item);
      }
      
      //no need declare @Transactional for queries because 
        //@Transactional(readOnly=true) is applied at class level
      public void findItem(Item item){
        itemRepository.find(item);
      }
```

## readOnly = true

By adding (readOnly =true) for query methods like findMember or
findAllMembers, it optimises resource usage by allocating just
the minimum amount of resources for querying.

Be careful **not** to use this for commands (updating or inserting)
because they will not work if this readOnly=true is added.



