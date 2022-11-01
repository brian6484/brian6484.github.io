---
layout: post
title: Safe Navigation Operator (?) in Thymeleaf to prevent NullPointerException
description: 
category: Thymeleaf
tags:
  - Thymeleaf

---

## Intro
Let's say we made a item register form for users to input 2 fields -
price and quantity. We want to validate these 2 fields if they indeed
make sense.

The server will check this validation logic when POST /add comes and
if it passes, it will use PRG pattern and redirect users to
Redirect /items/{id}. If it fails, the form will be shown again
to users and show what fields and errors, that are placed in Model
model) were made.


## Server validation logic
This is the server logic, very rudimentary:
```java
@PostMapping("/add")
public String addItem(@ModelAttribute Item item, RedirectAttributes 
redirectAttributes, Model model) {
    
   //검증 오류 결과를 보관
   Map<String, String> errors = new HashMap<>();
   
   //검증 로직
   if (!StringUtils.hasText(item.getItemName())) {
        errors.put("itemName", "상품 이름은 필수입니다.");
   }
   
   if (item.getPrice() == null || item.getPrice() < 1000 || item.getPrice() >
  1000000) {
        errors.put("price", "가격은 1,000 ~ 1,000,000 까지 허용합니다.");
   }
   
   if (item.getQuantity() == null || item.getQuantity() >= 9999) {
        errors.put("quantity", "수량은 최대 9,999 까지 허용합니다.");
   }
   
   //특정 필드가 아닌 복합 룰 검증
   if (item.getPrice() != null && item.getQuantity() != null) {
       int resultPrice = item.getPrice() * item.getQuantity();
       if (resultPrice < 10000) {
           errors.put("globalError", "가격 * 수량의 합은 10,000원 이상이어야 합니다. 
            현재 값 = " + resultPrice);
       }
   }
   
   //검증에 실패하면 다시 입력 폼으로
   if (!errors.isEmpty()) {
   model.addAttribute("errors", errors);
   return "validation/v1/addForm";
   }
   //성공 로직
   Item savedItem = itemRepository.save(item);
   redirectAttributes.addAttribute("itemId", savedItem.getId());
   redirectAttributes.addAttribute("status", true);
   return "redirect:/validation/v1/items/{itemId}";
}
```

HashMap is used to store the type of error as key and the error message
as the value. StringUtils.hasText is used to check validity of item
name.


## Thymeleaf's Safe Navigation Operator
Anyway, let's get back to the main point. 

```html
<div th:if="${errors?.containsKey('globalError')}">
  <p class="field-error" th:text="${errors['globalError']}">전체 오류 메시지</p>
</div>
```

We know .containsKey of HashMap but what is this ? question mark
in front of this method?

This question mark is known as the *safe navigation operator*.
Because "errors" can be null as users inputted all the valid fields,
without this operator, it can cause Null Pointer Exception.
So, to prevent this NullPointerException, safe navigation operator
is used to return null instead of this exception.
