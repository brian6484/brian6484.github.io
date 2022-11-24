---
layout: post
title: Difference between NotBlank, NotEmpty and NotNull when validating DTOs
description: 
category: Spring
tags:
  - Spring

---

## Why do we need to validate in the first place?
What if we enter an age into a name field? If we don't check
the validity of incoming data into our planned appropriate fields,
it may wreak havoc on the system.

## Example
Let's say we want a not-empty title for our post. We will use
@NotEmpty which checks not just empty string and null but also 
empty white space " ".

```java
public class PostRequest {

    @NotEmpty
    private String title;
    private String content;
    
    // ...
}
```

Then in our controller,
```java
@RequestMapping("/posts")
@RestController
@RequiredArgsConstructor
@Validated
public class PostController {

    private final PostService postService;

    @PostMapping
    public ResponseEntity<PostResponse> create(@RequestBody @Valid final PostRequest postRequest) {
        final PostResponse postResponse = postService.create(postRequest);
        return ResponseEntity.created(URI.create("/posts/" + postResponse.getId())).build();
    }
    
    // ...
}
```

Remember, Spring does not check the validity of DTO by us simply placing
an @NotEmpty annotation at one of DTO's fields. We have to place
@Valid annotation in front of the method parameter we want to validate
(i.e. in front of DTO). And add @Validated at Controller level.

When Spring Boot finds an argument annotated with @Valid, it automatically bootstraps the default JSR 380 implementation — Hibernate Validator — and validates the argument.

When the target argument fails to pass the validation, Spring Boot throws a MethodArgumentNotValidException exception.
Exceptions caused by validation causes *MethodArgumentNotValidException*
and causes 400 Bad Request (cuz it is the client's fault).

## Difference
### NotBlank
@NotBlank checks for null and empty values.
must be not null and their trimmed length must be greater than zero.
@NotBlank can be applied only to text values and validates that the property is not null or whitespace.
It is usually used to validate **collections**.

### NotEmpty
@NotEmpty is similar to @NotBlank but has 1 more validation functionality.
It checks for null and empty values but allows empty whitespace " ".
@NotEmpty validates that the property is not null or empty; can be applied to String, Collection, Map or Array values.
It is usually used for **String**.

Like @NotBlank, @NotEmpty 애노테이션은 위와 같이 길이가 0인 문자열로 요청을 보내면 에러가 발생합니다.
For example, "" causes error both annotations. But NotEmpty allows
whitespace " " and does not cause error. But NotBlank does not allow
whitespace " ".

### NotNull
It checks and rejects null values. It is usually used for
LocalDateTime.


## Reference
https://devlog-wjdrbs96.tistory.com/402
