---
layout: post
title: JPA 연관관계 편의 메서드
description: 
category: JPA
tags:
  - JPA
---
  
## Without convenience methods
Actually, JPA works just fine when we just input values into the
연관관계 주인. But it is not really Object-Oriented (OO) to just input
value at the Many side. Also, until transaction.commit can be invoked
and DB queries that data, the One side does not the know entity's
연관관계 so if we try printing out the data in One side, it is null.

For example, let's look at this:
```java
Team teamA = new Team();
team.setName("teamA");
em.persist(teamA);

Member memberA = new Member();
memberA.setName("memberA");

// memberA에 연관 관계 설정
memberA.setTeam(teamA);
em.persist(memberA);



System.out.println("memberA.getTeam : " + memberA.getTeam());
System.out.println("teamA.getMembers() : " + teamA.getMembers(0));
```

The last line does not run because in memberA, we set teamA but 
at the opposite side, teamA has not been mapped with memberA so it
does not have any member value.

So if teamA needs to know memberA, we have to do em.flush() and 
em.clear() to clear out PersistenceContext and force DB query to find
that value. This is more OO. I have discussed em.flush() and 
em.clear() [here](https://brian6484.github.io/jpa/2022/08/31/JPADBquery.html)

## With convenience methods
```java
@Entity
@Getter
public Member {
    
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "MEMBER_ID")
    private Long id;
    private String name;
    private Team team;
    
    public changeTeam(Team team) {
        
        // Member에 이미 Team이 설정되어 있을 경우
        if(this.team != null) {
         
            // team에서 해당 Entity를 제거
            this.team.getMembers().remove(this);
        }
        
        // 해당 member Entity에 파라미터로 들어온 team 연관 관계 설정
        this.team = team;
        
        // 파라미터로 들어온 team Entity에 member 연관 관계 설정
        team.getMembers().add(this);
    }
}
```

## Reference
[good ref](https://developer-rooney.tistory.com/223)
