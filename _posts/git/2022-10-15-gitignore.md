---
layout: post
title: How to use .gitignore to hide sensitive files in Spring Boot
description:
category: Git
tags:
  - Git
---

## Introduction
I made a horrible mistake in uploading my AWS secret key and access
key in my application.yml file to github repo. All chaos followed suit
as both AWS and Github sent me emails that my keys have been exposed.
And there were hacking attempts by bots to use my keys. 

Thus, it is a lesson to be learnt and I will discuss how to prevent
this.

## Just adding your file to .gitignore is insufficient
It can still be tracked by your repo branch. So to solve this, we need
to remove the cache that is being tracked. Then, we do a new commit
and the .gitignore will be applied on a fresh new leaf.

## Removing cache
Well we know this code:
```gitignore
git rm fileName
```

This deletes file in both local working directory and github repo.

But by using this tag called cache:

```gitignore
git rm -r --cached .
```

It deletes the file only in the github repo (not your working
directory) and removes file in the staging area. 

What is staging area?
It is in the middle of your working directory and repo, where 
all the added files for a commit are stored. It is when you do git add.
That is the staging area, right before you commit it to your repo.


## Solution
If you want to delete all the cached files, add the dot. But if you
want to delete a certain file like application-member-local.yml, this
is what you should do.

1) Copy the file path from **repository root** like module-member/src/main/resources/application-member-dev.yml
2) git rm -r --cached this_file_path
3) git add .
4) git commit -m "added this file to gitignore"
5) git push origin brian(name of ur origin branch)

Check repo if you indeed can't see the yml file. Also, the file
will be highlighted in a light grey colour if properly removed.

## .gitignore when working in a team
To be added

## Reference
https://velog.io/@gillog/Git-.gitignore-%EC%9E%AC%EC%A0%81%EC%9A%A9

