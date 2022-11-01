---
layout: post
title: Could not resolve placeholder 'test.name' in value "${test.name}"
description: 
category: application.yml
tags:
  - application.yml

---

## Error
When I was setting up S3 with my toy project in Spring Boot,
this dreadful error kept popping up.

> Could not resolve placeholder 'test.name' in value "${test.name}"

I met this dreadful error many times when setting up values of JWT
token by getting them from application.yml file so I was annoyed.

## Solution
Here was my wrong application-member-local.yml file.
```yaml
#above are the regular spring settings

cloud:
  aws:
    credentials:
      access-key: XX
      secret-key: XX
    s3:
      bucket: codingmates
      dir: /codingmates/hola
    region:
      static: us-west-1
    stack:
      auto: false
```

I thought there was something wrong with my multi-module architecture
and I tried placing this setting on all the relevant .yml files and not
just application-member-local.yml file.

It didn't work so I checked which configuration the project was running
on by default and it was running on 1)local, 2)member-local 3)project-local
4)skill-local, which are all the local modules + 1 common module.
So the configuration was fine.

What is the error then??

Turns out, when I was calling the value with @Value, I 
**misspelled the directory**, a very careless mistake. In my
AWSConfig class, I was calling it via accessKey (notice there is
no - between "access" and "Key") but in my yml file, I am calling
it via access-key (2 different variable names).

```java
@Configuration
public class AwsConfig {

    @Value("${cloud.aws.credentials.accessKey}")
    private String accessKey;

    @Value("${cloud.aws.credentials.secretKey}")
    private String secretKey;
}
```

So I corrected the names to accessKey and secretKey in my yml file
and it worked!

