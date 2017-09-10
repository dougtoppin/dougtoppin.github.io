---
layout: post
title: "AWS Config Service"
date: 2014-11-15 21:31
comments: true
categories: [aws]

---
I am a strong believer in the AWS but have felt for some time that an important utility for it was missing.
It is easy to configure a variety of resources in the AWS but keeping a record of your current configuration for tracking changes or disaster recovery involves using various describe commands to get the configuration.
Amazon recently announced their new AWS Config service which enables the user to be notified (via AWS SNS) of configuration changes and will record the configuration state itself at intervals.

The configuration is captured via files sent to an S3 bucket with the files being associated with the various aspects of your AWS usage.
Examples of them are CloudTrail, EC2::Instance, EC2::SecurityGroup and EC2::Volume.
The contents are json formatted entries describing the resource.

If you are not currently capturing all of your AWS resource configuration you should consider what would happen if portions of it were inadvertantly (or intentioanlly) deleted and how difficult it would be to restore everything back to normal.
