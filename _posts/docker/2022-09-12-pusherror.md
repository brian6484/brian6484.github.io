---
layout: post
title: docker push denied: requested access to the resource is denied
category: Docker
tags:
  - Docker
---

Let's dive in 
## Issue
```yaml
Using default tag: latest
The push refers to repository [docker.io/asdfaasdf/kubia]
6bb2a0932f1d: Preparing 
ab90d83fa34a: Preparing 
8ee318e54723: Preparing 
e6695624484e: Preparing 
da59b99bbd3b: Preparing 
5616a6292c16: Waiting 
f3ed6cb59ab0: Waiting 
654f45ecb7e3: Waiting 
2c40c66f7667: Waiting 
denied: requested access to the resource is denied
```

When I was trying to push my image to Docker Hub, there was this
request access deny error.

2 main reasons why - 1) I did not login to Docker Hub 
2) My docker hub's id and the tagged image's name does not match

For me it was the latter. But let's see the solution for both.

## Solution 1
Login to Docker Hub
```yaml
$ docker login           
Login with your Docker ID to push and pull images from Docker Hub. If you dont have a Docker ID, head over to https://hub.docker.com to create one.
Username: bcp0109
Password: 
Login Succeeded
```

But if you are using Docker Hub cuz ur OS is Windows, just logging
in to the Docker Hub UI is sufficient.

## Solution 2
Match the tag with the ID.
```yaml
$ docker tag codingmates brian6484/codingmates
$ docker push brian6484/codingmates     
```

It works!



