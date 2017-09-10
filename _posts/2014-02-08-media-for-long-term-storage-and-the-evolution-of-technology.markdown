---
layout: post
title: "Media for long term storage and the evolution of technology"
date: 2014-02-08 10:26
comments: true
categories: 
---
One thing that I've seen over years is how media technology evolves and is outmoded (tape, floppy, cd, dvd, flash drive) by more modern technology formats or storage (cloud).
The result is that you end up with old media that is difficult or even impossible to access or has failed.
For example, I have a few old CDs of band music from my high school days and DVDs of family movies.
However my MacBook Pro (my only machine now) does not have a DVD (saves weight, cost).
This has not caused me any problem but if I needed to access any of that old media it would be a little bit of a pain.
I could transfer them to USB flash drives but that will likely also eventually disappear and they might fail so I would need at least two copies of each.
I've been thinking about ways to address this and I've decided to send them all up to the Amazon AWS Glacier facility (cloud storage).
The pricing for that is currently $0.01 per GB per month (cheap as long as you are willing to potentially wait for a few hours to access it).
Advantages of this include that it is inherently safe (replicated), Internet accessible and the storage media will never disappear.
Internet access bandwidth will only increase in the future making it a quicker transfer when I actually do need it.
I also bought a good scanner (Fujitsu S1500M) a while back and went to a paperless office at home.
I may move those files up there as well.

A few observations in the near term follow

* pros
  + cheap
  + reliable, somebody else ensures that it is replicated/backed up so you don't have to
  + intended to hold large volumes of data
  + secure, it is encrypted on the server so you don't have to
* cons
  + slow access, maybe a few hours before it is ready once you decide that you need it
  + no user-friendly built-in user interface, you have to some form of code
  + Glacier assigns an identifier for the object, you do not refer nor find it by your file name, in 10 years you might have trouble figuring out what is what unless you keep a list somewhere

This will be an interesting experiment to see how my file cabinet in the sky (cloud?) will work out for me.
Check back with me in 10 years and I'll let you know or else here every now and then for when I post more updates.

