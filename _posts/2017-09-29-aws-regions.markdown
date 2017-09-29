---
layout: post
title: "Do you check your AWS regions when looking around?"
date: 2017-09-29 15:14
comments: true
categories: [blog]
description: When you are checking for anything unused (or unusual) in your AWS account do you check all of the regions that exist? You probably should.
keywords: aws
---

I just discovered something interesting.
Typically I browse the work aws account to see what instances are running, vpcs exist and so on.
I pretty much only do that with us-east selected.
I just discovered that we have, for some unknown reason, a few vpcs created in other regions and are not being used.
it is probably a good idea to script the cli, implement a config service rule or something else to scan all regions for stuff that might exist in your account that have been forgotten about.
The intent being to reduce wasted expense and account cruft in general.

I also wonder how easy it might be to have ec2 instances, databases or whatever existing in other regions that might be costing money without your knowing or noticing.
So, let’s say someone gets your account credentials.
Rather than do something that would attract attention they instead select a region that you do not use and create stuff in there. how long would it be before you notice it?

More to come on this.


