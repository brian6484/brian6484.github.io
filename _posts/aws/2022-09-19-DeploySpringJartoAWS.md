---
layout: post
title: How to deploy Spring jar app to AWS
category: AWS
tags:
  - AWS
---
Finally arranging this so that I don't have to google it again.

## Intro
We are using Ubuntu server with Spring jar. So the linux commands will
all be "apt-get".

## Build jar file
On the right tab of IntelliJ, click Gradle -> Build -> Build.
Click on that grid icon and jar file will be built in the libs folder.

## FileZilla to move jar file
Once you build successfully, there will be 2 jar files. Choose
the SNAPSHOT.jar file, NOT the SNAPSHOT-plain.jar.

> SNAPSHOT.jar 는 실행가능한 아카이브이고, SNAPSHOT-plain.jar 는 실행이 불가능한 일반 아카이브이다

## Initial server configuration and downloads
Once you access through SSH:
```yaml
sudo apt-get update
sudo apt-get install openjdk-11-jdk //스프링 부트 버전과 맞춰서 설치한다.
java -version //버전 확인
```

## Double check security group of EC2
Remember my Django project's SG did not allow port 8000 and I was
wondering where the error was so mistake learnt!

Tomcat runs on 8080 by deport so SG of our server should allow 8080
and 80 (HTTP) and 443 (HTTPS).

## Migrate jar file through FileZilla
Click new Site, and for protocol, choose FTP file transfer protocol.
Then add ubuntu as username and key file as password. Then, make
a directory on our EC2 server and move the built jar file in there.

## Run the jar file on EC2
```yaml
java -jar 파일이름.jar
```

You probably wanna run the dev environment, not local. Also, if
your project is multi-module:

```yaml
java -jar -Dspring.profiles.active=dev [jar file name].jar
```

Again, like setting up configuration for running java application,
no need to type every dev profile like dev, member-dev, project-dev, etc.

## Run server 24/7
```yaml
nohup java -jar 파일이름.jar &
```

If you want to kill the server and stop it from running, first
identify the process *number* through this command
```yaml
ps -ef | grep java
```

Once you identified the number, you can kill it via:
```yaml
kill -9 the_process_number
```
