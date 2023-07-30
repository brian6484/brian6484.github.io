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

## all the 연관된 entities have to be in managed state

To save entities in 연관관계, **all the 연관된 entities HAVE to be in managed state (i.e persisted by EM)**

```java
Team team = new Team(“team1”)
em.persist(team)

Member member1 = new Member(“brian”)
//team is persisted and in managed state so can do this
member1.setTeam(team1)
em.persist(member1)
```

Important confusion: wait I thought em.persist() stores all the SQL 
queries in SQL저장소 and it is only when em.flush() that the SQL queries 
are sent to DB? So here, don’t you need em.flush() before member 
can setTeam(team1)?

It is correct that SQL queries are stored in SQL저장소 and not sent to 
DB yet when em.persist() happens. But as mentioned, the entities only 
have to be in **managed state** via EM , not actually saved in DB.

For the flush bit, I am still confused. OHHHH flush is called after 
persist in certain cases, according to ChatGPT.

## for bi-directional 연관관계

For bi-directional 연관관계, only the 연관관계 주인 is mapped with DB 
연관관계  so can manage the FK. Owner can create, update or delete. 
But the opposite side can only read

Emphasis: common pitfall is entering values not on the 연관관계 owner but 
the opposite side. ONLY the owner can change the value of FK

member1.getTeam().add(team1) works bcos Member is owner
team1.getMembers().add(member1) will NOT work and team_id will be NULL cuz only the owner can change the value of FK

But thinking OOP without JPA, it is only right to set values on BOTH sides as if we set only 1 side, it will not work for that side. So following OOP, best practice to set values on both sides like

```java
member1.getTeam().add(team1) works bcos Member is owner
team1.getMembers().add(member1)
```

Although team.getMembers.add will not work anyway, it is OOP design

As mentioned we need to consider both sides and set values on both sides.
If we call the methods separately like

```java
member1.getTeam().add(team1)
team1.getMembers().add(member1) 
```
it might cause unintentional error.

So best practice is that for 양방향, it is best to use these 2 codes 
like one function.

for Member
````java
Private Team team;
Public void setTeam(Team team){
This.team = team;
team.getMembers().add(this);
}
````

HOWEVER, when we do
```java
member1.setTeam(team1)
member1.setTeam(team2)
Member findMember = team1.getMember();
//member1
```

Team1 still has member1 in it because teamA -> member1 
(teamA referencing member1) relationship is not removed. When we want 
to update 연관관계 from teamA to teamB, if there is an initial team 
(of teamA), we need to remove that 연관관계 like

Member

```java
private Team team;

public void setTeam(Team team){
    if(this.team !=null){
        this.team.getMembers().remove(this);
    }
    
    this.team = team;
    team.getMembers().add(this);
  }

```

}

BTW, even though teamA->member1 reference relationship is not removed, 
there is no problem to change FK value. This is because Team.members, 
which sets the reference relationship of teamA->member1 is not the 
연관관계 owner. FK value is changed accordingly cuz member.team set 
ref relationship of member1 -> teamA.

When EM is renewed and in new persistence context, teamA.getMembers() 
is null cuz FK relationship is cancelled. Issue is when the reference 
relationship is changed (teamA to teamB for member1) and in that same
PC(where it is not renewed or closed), member1 is returned. So anyway 
it is safe to use this 편의 method.

Also v important, you can put 2 편의 methods for both sides like setTeam 
and addMember but if have both sides, may go into infinite loop. Just 
call one 편의 method.


## Reference
[good ref](https://developer-rooney.tistory.com/223)
