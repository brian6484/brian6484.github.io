---
layout: post
title: ThreadLocal to change Hibernate's query manually
category: Spring 
tags:
  - Spring

  
---
##Issue
Let’s say you need to change the parameter name while Hibernate makes the sql query for you. How do you do that?

For example, we want to change some_log_table to some_log_table_20230303. How?

We use ThreadLocal to pass in the parameter to Hibernate’s interceptor as such

```java
threadLocal.set(formattedDate)
```

And once the formattedDate is finished being used and sql query has been formed, we remove threadLocal

```java
threadLocal.remove();
```

