---
layout: post
title: A MUST check when setting up AWS RDS (or you will get Fatal Error 3000:0 - No such database found)
category: AWS
tags:
  - AWS
  
---

I have faced this problem multiple times when setting up AWS RDS. When I tried connecting to 
DB for the first time (via IntelliJ), there was this error:

## Fatal Error 3000:0 - No such database found

Solution: Please please please! Make sure to **initialise** database name at the *additional
configuration* section at the end of the set-up page. It is tucked away and you have to 
click and open it up to name your db. If you don't do this, AWS actually does not 
create this DB and they even mention this in that section.

Also, be careful and remember the name of the db you are setting
up. Like hyphens or underscores can mean the difference!
E.g. my_db != my-db 

## How to properly set up RDS
1) DB instance identifier - give it the SAME name as the
initial database name in the *additional configuration* section,
just in case
2) In connectivity section, MUST MAKE it PUBLIC ACCESS. Don't
connect to EC2 compute resource and give it public access. You can
connect your EC2 after creating and connecting RDS after you see
it working.
3) Create new SG and don't put any inbound rules yet until
you create your RDS. After you have created your RDS,
go to the SG of RDS and add inbound rule of your IP and
custom TCP port. If you have fellow developers that need
access, add another rule allowing all ipv4 traffic.
4) **VERY IMPORTANT** *initialise* database name at the
*additional configuration* as mentioned in the above sub-section
with the same name as DB instance identifier
5) Remember your Master username and password when creating RDS
   (e.g. username is postgres, password is blalbal)


## Connect RDS to IntelliJ
Host: RDS endpoint

User & password: master username and password (e.g. postgres, blabla)

Database: the "initial database name" you have created in the
additional configuration section
