---
layout: post
title: "AWS images/backups and lessons (re-)learned"
date: 2014-04-17 16:59
comments: true
categories: 
---
A recent hard lesson learned (again) prompted me to put up a post.
Off and on over a period of days I configured an AWS EC2 instance with a logstash server to act as a log file aggregator.
It was running redis (to collect), logstash (to index), elasticsearch (to provide a search api) and kibana (the UI).
I had a number of logstash agents sending various log files to it which was very convenient for providing a central place to find logs rather than having to ssh to individual instances and then find the file of interest.
It was working pretty well and I kept meaning to get around to both backing it up and documenting the configuration.
I was the only one working on it so I figured that as long and I did not mess it up it would be safe.
Unfortunately, someone else accidentally terminated it causing me to spend almost two days to get it back up and working again.
The issues with getting it back up were primarily which version of each tool I had originally used and then what the configuration of each was (having only a vague memory of them).
Another aggravation was the loss of weeks of historical data that I was hoping to use someday for some data analysis.

The lessons learned again included:

* use EC2 'create image' at intervals to keep a backup of the instances that you might have to manually reproduce someday
* keep some reasonble records of what is on them and how they are configured, in fact pulling the configuration directly from a git repo is desirable if possible
* export and backup data files to the S3 in case you want to use them again someday for something else
* consider using things like CloudFormation or the Elastic Beanstalk and .ebextensions to stand up and configure your servers, these provide quicker standup as well as documenting how they are configured
* get around to setting up more granular IAM roles to prevent accidental access (this is more difficult than it sounds in small team environments where anyone might need to do something to anything)
* always recognize that in cloud environments that your instances and stuff might suddenly go away for any number of reasons, ensure that you know how to get them back up reasonble quickly, it is someone else's problem until it becomes your problem

