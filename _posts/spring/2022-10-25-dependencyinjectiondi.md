---
layout: post
title: What is Dependency Injection and how to do it via constructor?
category: Spring
tags:
  - Spring

---
## DI
It refers to a specific implementation of Spring's IOC container
that is used to reduce dependencies between objects.

A reminder of IOC is that the IOC container, not the developer,
manages the instance from creation to destruction. This 
IOC container is injected through DI.

## Java bean
Java objects created and (destroyed eventually) managed by spring IOC container is called bean.

## Analogy of DI
To go with your analogy of your components being in a treasure chest: A system (lets say a treasure polisher) without dependency injection has to have the ability to pick an item from the treasure chest itself. It has to have some knowledge the dependency's nature in order to pick the correct treasure to polish depending on the current context. Thus coupling.

In a DI scenario, your treasure polisher does not need to know about the existence of the treasure chest at all. All it needs to know is that at some point (preferably at creation) the polisher will be provided (injected) with an object which implements ITreasure:

## 3 ways of DI
There are 3 types: field injection, setter injection, and constructor injection
but constructor is highly recommended.

### Field injection
It cannot modify field objects. Also, to use this, we have 
to rely on DI framework (e.g. Spring)
```java
@Autowired 
private UserRepository userRepository
```

## Dependency Injection through constructor
Advantages:
1) Constructor injection injects required beans at the time 
of object creation with a constructor. Therefore, the 
circular reference can be solved. **But it can still occur**.
When it does occur, best solution is to 순환참조가 되지 않도록 설계.
Last resort is putting @Lazy annotation, though it is not
recommended at all by Spring.

2) Fields can be declared final. So can make them immutable

3) You can run tests more easily without using a DI container 


Various methods like setter method are used in DI. But DI through constructor is most recommended.

 ```java
    public class MemberService {

        private final MemberRepository memberRepository;

        @Autowired
        public MemberService(MemberRepository memberRepository) {
            this.memberRepository = memberRepository;
        }
 ```
And then when you want to DI:

 ```java
    public WebConfig(){
        MemberService memberService = new MemberService(bitchMemberRepository);
    }
 ```
## Better way
But a better way is remembering that @Autowired can be omitted if there is **only one constructor** and using Lombok's @AllArgsConstructor:

  ```java
    @AllArgsConstructor
    public class MemberService {

        private final MemberRepository memberRepository;
  ```

## Best way
Best way is using @RequiredArgsConstructor, which creates constructor only for @final or @NonNull field. When there is just 1 constructor, @Autowired is automatically added to that constructor for DI:

  ```java
    @RequiredArgsConstructor
    public class MemberService {

        private final MemberRepository memberRepository;
  ```

Another example of DI:
  ```java
    @Repository
    @RequiredArgsConstructor
    public class MemberRepository {

    //    @PersistenceContext
        private final EntityManager em;
  ```
which is same as:
  ```java
    @Repository
    public class MemberRepository {

        @Autowired @PersistenceContext
        private final EntityManager em;

        public MemberRepository(EntityManager em){
            this.em = em;
        }
  ```

