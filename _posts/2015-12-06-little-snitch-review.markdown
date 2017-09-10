---
layout: post
title: "Little Snitch Review"
date: 2015-12-06 19:56
categories: [technology, review]
description: Using Little Snitch To Monitor and Control Network Connections
keywords: technology, little snitch

---
A few observations from using Little Snitch (LS) 3.6.1 on my MacBook Pro (MBP) running El Capitan.
LS is used to monitor and control network connectivity from your computer.
The intent is to prevent or allow applications that you may not realize to contact other servers.

It is eye opening to see how many outbound connections happen.
On first boot after installation there are a boatload  of approvals necessary to get back to everything working.
All except LS known required connections are denied.
Once you start the approval process you choose if to allow temporarily or permanently to the same destination using the same port.
Some of these are not using permanent ports so for those you decide if to allow any port to the same destination type thing.
It is not difficult but might add to any paranoia you might already have.
I would not recommend it for a non-technical person at least yet unless someone is able to help them.
It is also a good learning experience for the technical for a variety of reasons including thinking about your app connectivity and how it might be impeded by the installation configuration.

It is also a well done UI in terms of clearly showing what is going on in your system. The real-time view is also well done and interesting.
It shows connection activity at any moment.

You may find, like I did, that you at least initially approve everything just to get back to a normal working condition.
Also note that initially not every application that you use will be active so over a period of hours or even days you may have to allow connections from them.
This will also likely be true for applications that you use at the shell level.
After a while you may start tailoring the rules for it and you may also delete a few applications that you don’t think are essential to your normal work flow because of them “reporting back” to someone, somewhere.

All in all I would recommend LS if you are interested in the subject and/or want to know what your system is doing and to control it.
