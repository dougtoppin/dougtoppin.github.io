---
layout: post
title: "don't test in production"
date: 2013-12-07 22:24
comments: true
categories: 
---
Last weekend I inadvertantly cause a problem in a production system (AWS) by doing something that I thought that I understood and it turned out that I did not.  The lesson that I (re)learned was "don't test in production, even if you think that you are not testing".  I should have tried what I was going to do on a test instance before doing it in prod.  As usual, causing and fixing a problem taught me how EIPs really work in the AWS but I would have preferred to read about it rathen than cause it.  I was thinking that I could associate an EIP with a running EC2 instance without impacting the existing IP for it.  What actually happens is that the previous IP is lost and the EIP is immediately associated.  This means that anything that you were doing using the old IP will no longer work and you have to start using the new IP.  Since that can cause confusion it is preferable to do this in a coordinated and controlled fashion rather than willy nilly.  Note that if you try to back out the change by unassociating the EIP the instance will not longer have a public DNS entry and IP at all (leaving you in the proverbial pickle because you can't ssh to it at that point).  Once you associate the EIP you are pretty much committed to using it until you make some other change.

