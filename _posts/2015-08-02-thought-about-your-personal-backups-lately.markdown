---
layout: post
title: "Thought About Your Personal Backups Lately?"
date: 2015-08-02 23:09
comments: true
categories: [aws, glacier, backups]

---
A recent hard crash of an old iMac last week made me realize that I had exactly one copy of a iPhoto archive (now Photos) that covered numerous years up to 2012.
I had moved that iPhoto library from my MBP to an external drive in 2013 and started a new one on my MBP because it was getting so large.
I decided to send both libraries to AWS Glacier using Arq.
I had been using Arq previously to back up a tarball of a set of family photos but that was pretty static and just on autopilot so I decided to up my usage to include these archives.

I know that I could use (and do for other files) an external drive with TimeMachine but I wanted the confidence of offsite and replicated storage for these pictures that would likely be impossible to find again if I lost them.
Glacier is the perfect candidate for that on a personal level as well as my professional use.

More to come on this as I evaluate Glacier (and Arq) for my Photos libraries.
I am particularly interested in the monthly cost and rate of change as photos are added.
I am guessing that this will also cause me to get in the habit of one Photos library per year from now on.