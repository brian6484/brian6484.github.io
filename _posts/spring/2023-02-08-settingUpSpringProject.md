---
layout: post
title: Set up directories in your Spring project properly
category: Spring
tags:
  - Spring
  
---
## The error
How I knew about this was through an error in test case.
@Autowired was not working for my test case. The error of 

>"could not autowire no beans of type repository found test case"

kept popping up. StackOverflow recommended a 
@ComponentScan(basePackages=”com.gbc.atdd.repository”) but still, it 
didnt work. 

## Solution
Turns out, the issue was the misplacing my directories of repo, service 
and domain. Directory/location of my main Application.java file was under 
com.gbc.atdd.ibsos. I added my other directories 
(like domain, service, repo) at the **same hierarchy level** as ibsos. 
My directories should have been below ibsos directory like com.gbc.atdd.ibsos.repo

If you want to keep the same hierarchy level, you should add 
@SpringBootTest(classes = IbsosApplication.class) at the Test case class. 
But if you have just a few files to move around, I recommend just 
moving them.
