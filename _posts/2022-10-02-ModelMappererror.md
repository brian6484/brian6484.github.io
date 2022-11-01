---
layout: post
title: Parameter 1 of constructor in Service class required a bean of type 'org.modelmapper.ModelMapper' that could not be found.
subtitle: Spring
category: Spring
tags:
  - Spring
---

## Initial wrong code
```java
public class AppConfig {
    @Bean
    public ModelMapper modelMapper(){

        return new ModelMapper();
    }
}
```

## Solution
I have not properly registered my Bean. Whilst I declared my ModelMapper as bean method,
I have not annotated my class with @Configuration.

```java
@Configuration
public class AppConfig {
    @Bean
    public ModelMapper modelMapper(){

        return new ModelMapper();
    }
}
```

