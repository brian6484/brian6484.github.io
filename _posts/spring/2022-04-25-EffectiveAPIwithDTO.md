---
date: 2022-04-25 14:35:23
layout: post
title: How to create effective APIs with DTO? 
description: 
category: Spring
tags:
  - Spring

---

## Intro
Exposing our entities (Member, Project, Item) to our controllers is very dangerous
and is a big NO-NO! So how do we set up controllers and DTOs?

## API Version 1 - Using Entity as parameter
```java
@RestController
@RequiredArgsConstructor
public class MemberApiController {
   private final MemberService memberService;
   /**
   * 등록 V1: 요청 값으로 Member 엔티티를 직접 받는다.
   * 문제점
   * - 엔티티에 프레젠테이션 계층을 위한 로직이 추가된다.
   * - 엔티티에 API 검증을 위한 로직이 들어간다. (@NotEmpty 등등)
   * - 실무에서는 회원 엔티티를 위한 API가 다양하게 만들어지는데, 한 엔티티에 각각의 API를
  위한 모든 요청 요구사항을 담기는 어렵다.
   * - 엔티티가 변경되면 API 스펙이 변한다.
   * 결론
   * - API 요청 스펙에 맞추어 별도의 DTO를 파라미터로 받는다.
   */
   @PostMapping("/api/v1/members")
   public CreateMemberResponse saveMemberV1(@RequestBody @Valid Member member) {
       Long id = memberService.join(member);
       return new CreateMemberResponse(id);
   }
   //dto for version 2
   @Data
   static class CreateMemberRequest {
        private String name;
   }
   
   @Data
   static class CreateMemberResponse {
       private Long id;
       public CreateMemberResponse(Long id) {
       this.id = id;
       }
   }
}
```

There are several problems with this
1) Logic to check the validity of API is *inside* the entity (e.g.@NotEmpty field in
our Member's name field)
2) In real life, there can be many different APIs for the Member entity but to fulfill
every API's requirement by placing the logic inside our Member entity is impossible.
3) When entity changes, our API 스펙 changes.

Thus the solution is to get DTO as a parameter to adjust to API request 스펙s.

## API Version 2 - using DTO as API pararmeter
```java
@PostMapping("/api/v2/members")
     public CreateMemberResponse saveMemberV2(@RequestBody @Valid
        CreateMemberRequest request) {
        Member member = new Member();
        member.setName(request.getName());
        Long id = memberService.join(member);
        return new CreateMemberResponse(id);
 }
```

Now, instead of Member entity, we have CreateMemberRequest as the parameter that is
mapped with @RequestBody.

Advantages:
1) Entity and 프레젠테이선 계층을 위한 logic can be separated.
2) Entity and the API 스펙 can be separated.
3) If entity's field is changed, the API 스펙 is not changed.

So we can add @NotNull in the DTO's name field for API 스펙 and effective 유지보수.
If you added @NotNull in the *entity*'s field like version 1, it is hard to differentiate
APIs because not all the APIs may need a @NotNull name, which is according to each API
스펙.

```java
   @Data
   static class CreateMemberRequest {
        @NotNull
        private String name;
   }
```


