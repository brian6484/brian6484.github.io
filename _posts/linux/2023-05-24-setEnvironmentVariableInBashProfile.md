---
layout: post
title:  How to set environment variable in bash profile in linux
category: Linux
tags:
  - Linux
---

## Solution
### no space in between!
when setting environment variable in bash profile, VERY IMPORTANT 
DON’T PUT space in between anything. There should be no space like 

env_var=blah, not env_var = blah.

For example,
```yaml
Export LD_LIBRARY_PATH=${LD_LIBRARY}:/home/brian/bitch
Export JAVA_HOME=/home/brian/jdk/jdk1.8.0_371
Export PATH=$JAVA_HOME/bin:$PATH
```


Wrong:
```yaml
Export LD_LIBRARY_PATH  =  ${LD_LIBRARY}:/home/brian/bitch
#Notice the space in between var and = 
```

### don't forget to save your changes!
Once you have set environments you want to save it via
```yaml
vi .bash_profile 
#and to set the changes, 
source .bash_profile
```



