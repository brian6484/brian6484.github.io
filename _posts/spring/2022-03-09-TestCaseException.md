---
date: 2022-03-09 14:35:23
layout: post
title: How to test exception in test cases
description: 
category: Spring
tags:
  - Spring

---

## Testing exceptions
You can do this by adding the expected exception class to the
@Test annotation.

```java
@RunWith(SpringRunner.class)
@SpringBootTest
@Transactional
public class MemberServiceTest {
   @Autowired MemberService memberService;
   @Autowired MemberRepository memberRepository;
 
   @Test(expected = IllegalStateException.class)
   public void 중복_회원_예외() throws Exception {
   //Given
   Member member1 = new Member();
   member1.setName("kim");
   Member member2 = new Member();
   member2.setName("kim");
   //When
   memberService.join(member1);
   memberService.join(member2); //예외가 발생해야 한다.
   //Then
   fail("예외가 발생해야 한다.");
   }
}
```

Pay attention that there is this *fail* that you can add with your message 

## More on Testing annotations
Look at [my post](https://brian6484.github.io/java/2022/09/19/JPArepo.saveNullPointerException.html)
which explains @RunWith, @SpringBootTest, and @Transactional more closely.

## Setting a separate yml file for testing
I didn't know you could actually set up a separate yml file for testing.
Place your file in test/resources/application.yml.

