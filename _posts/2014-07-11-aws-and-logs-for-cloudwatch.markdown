---
layout: post
title: "AWS and Logs for CloudWatch"
date: 2014-07-11 21:04
comments: true
categories: 
---
Amazon recently announced a new feature that may save you some effort if you are a Logstash user.
Logstash is commonly used as a log file aggregator where Logstash, redis, elasticsearch and kibana are combined to support the collection, indexing and access of log and other files.
The feature that Amazon announced with the AWS Logs for CloudWatch facility.
Logs for CloudWatch is a simple to install package which installs an agent that can be easily configured to send (or ship in the Logstash vernacular) logfiles to the CloudWatch service.
You can then view the log contents via CloudWatch.
An advantage of this is that if you are already a user of CloudWatch then you are able to use the filters and so on to act on your logs.
You also do not have to go through the effort of the installation and configuration of the individual pieces of the Logstash stack.
Drawbacks of moving from Logstash to CloudWatch include no longer having the apis of redis and elasticseach which can be consumed by various tools as well as the much improved kibana user interface.
It's likely that CloudWatch will continue to improve and provide all sorts of neat features but right now it may be convenient to just get more of your stuff into the AWS ecosystem and find ways to make even more use of it.
The installation of the agent package is easy and it starts working very quickly once you tell it what logs to capture.
I also had no trouble in installing the agent on a DigitalOcean Ubuntu instance and configuring it to send log data to CloudWatch.

All in all this is another example of how Amazon continues to improve the AWS and give you more opportunities to explore it.

