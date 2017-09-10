---
layout: post
title: "AWS EC2 /etc/sudoers lesson learned"
date: 2013-10-28 22:15
comments: true
categories: 
---
I had a lesson learned that taught me a few things that are worth passing along.  I was doing some Zabbix work with an EC2 instance and needed to add something to /etc/sudoers to let Zabbix run a new script.  I quickly went in to it with 'sudo vim /etc/sudoers' made the addition, saved the file and exited vi.  I almost always use visudo but since this was a very small change I did not (doh).  After exiting vi I tried running the script using sudo and it said that there was a syntax error in sudoers.  I tried to edit it again using sudo and go the error again and I said "uh oh".  In the past, I've made this mistake on a local Linux system that I could quickly fix myself by either logging in as root or booting single user and fixing it manually.  Unfortunately you cannot do that in the EC2.  Before long I realized that I might have really "messed things up".  I had to contact a system administrator (that was on vacation) and asked for help.  He was able to fix it before long but the fix is not particularly easy and does involve some luck.  The fix is to ssh to another EC2 instance that has access to the same EBS (the disk space), mounting the disk and editing the remote file using the other instance.  This corrected the problem but I realized the lesson(s) learned are:

-  the obvious one of don't directly edit sudoers and instead use visudo like you are supposed to
-  have another means of getting to root other than by sudo and use it only when you have no other choice
-  have a failover strategy that you regularly test in case you lose a machine entirely
-  be able to reproduce the current state of any machine in case you suddenly lose a critical one
-  have a documented procedure for things like that so that you are not 100% dependent on a single individual that may not be in the office
-  the obvious one of don't directly edit sudoers and instead use visudo like you are supposed to

This mistake was embarassing and I learned my lesson this time.  There isn't a reason to directly edit that file.  visudo will perform at least some syntax checking to ensure that you are not leaving the file in an unusable state.

