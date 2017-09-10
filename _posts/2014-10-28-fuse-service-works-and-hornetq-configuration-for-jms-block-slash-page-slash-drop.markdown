---
layout: post
title: "Fuse Service Works and HornetQ Configuration for JMS BLOCK/PAGE/DROP"
date: 2014-10-28 13:19
comments: true
categories: 
---
If you are using Red Hat Fuse Service Works with the default HornetQ broker you should be aware that by default HornetQ is configured to have JMS writers block when a message queue fills (fill being defined by the maximum number of bytes allowed for the queue).
This document is particularly useful in learning a bit more about the configuration of HornetQ particularly associated with the paging of JMS messages

[http://docs.jboss.org/hornetq/2.3.0.Final/docs/user-manual/html_single/#paging](http://docs.jboss.org/hornetq/2.3.0.Final/docs/user-manual/html_single/#paging)

In particular note that the setting of *<address-full-policy>* is key to how the queue will be managed.
This can be set to any of these values *BLOCK, PAGE, DROP*

*DROP* tells the broker to not enqueue any additional messages once the queue has reached the maximum allowed.

*BLOCK* will cause the sender to potentially block when trying to send to a full queue, potentially not the behavior that you are looking for.

*PAGE* will cause paging files to be created in a unique directory under *jboss-eap-6.1/standalone/data/messagingpaging/* with the contents being files named simiar to *000000042.page*.

The paging directory should also contain the file *address.txt* which will hold the actual name of the queue.

The behavior of paging will allow paged messsages to be dequeued as soon as a consumer is able to.

JMS in general is a highly configurable means of performing many functions but you should be aware of what configuration settings are in effect and how they may impact your application or system.



