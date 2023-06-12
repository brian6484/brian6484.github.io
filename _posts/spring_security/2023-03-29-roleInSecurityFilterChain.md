---
layout: post
title: Declaring role in SecurityFilterChain (I struggled with this a lot)
category: Spring 
tags:
  - Spring
  - Spring Security
  
---
## Problem
Fuck this /listAdminView. So in my SecurityFilterChain, I explicitly 
specified only the roles of Admin to be able to access this page. I 
thought there was something wrong with my implementation so I tried all 
sorts like

```java
.antMatchers(“/users/listViewAdmin”).hasRole(ADMIN.getValue))
```

I checked my DB and UserStatus of ADMIN was saved just fine. Then I 
tried debugging and UserSecurityService when I realised this was the 
issue. I actually **didnt add authority** to my user found from DB in 
my loadUserByUsername function. So the UserDetails that is returned 
from my function had username and password but no authorities. It 
doesnt matter if we saved a user with ADMIN. We have to assign that 
ADMIN role to the user that is found via username from 
loadUserByUsername function because SecurityFilterChain finds that user.

## Solution

```java
List<GrantedAuthority> authorities = new ArrayList<>();
if(user.getUserStatus().equals(UserStatus.ADMIN)){
authorities.add(new SimpleGrantedAuthority(UserStatus.ADMIN.getValue())
  
//  elif if there is other role like UserStatus.BASIC, same logic
  
  
  return new UserAdapter(user)
}
```

This is not it. It is also not
.hasRole(ADMIN) because hasRole() actually adds prefix ROLE_ infront 
of the string parameter that is passed in. So it is incorrect because 
our UserStatus is in the form of ADMIN(“ADMIN”). So use 
.hasAuthority(ADMIN.getKey()) to get the key of ADMIN, which is 
ADMIN (string). ADMIN.getValue() also works because it is also 
ADMIN(string).

In your html. infront of # like
${!#string.equals(a,b)}

For example, if you wanna show something only to admin ON THE SAME PAGE
where admin and basic can access that page, we do 

```html
<tr
th:if="${#strings.equals(userAdapter.user.userStatus,'ADMIN')}"
and ${!#string.equals(user.userStatus,'SUPERADMIN')}"

th:each = "user:${userDetailResponseDto}">
<td th:text = "${user.id}"></td>
```

Or your home page, if you want to show a button only to authenticated 
and authorised BASIC users, 

```html
<div sec:authorize="isAuthenticated()">
  th:if = "${string.contains(#authentication.principal.authorities,'BASIC')}">
  only authenticated and basic users can see
</div>
```


