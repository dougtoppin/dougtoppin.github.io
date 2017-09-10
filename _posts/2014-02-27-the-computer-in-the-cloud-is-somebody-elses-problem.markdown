---
layout: post
title: "The Computer in the Cloud is Somebody Else's Problem or AWS CloudTrail and What Happened?"
date: 2014-02-27 12:48
comments: true
categories: 
---
A recent experience got me to thinking about AWS usage a little more and I wanted to pass it along.
An EC2 instance had an apparent unexpected reboot recently and I needed to look into why it happened.
Being somewhat paranoid (I know you are watching me through my webcam right now) I wanted to ensure that it was not due to any kind of hacker activity which was my first concern.
I checked /var/log/secure and /var/log/messages to see if anything unusual was going on and that did not appear to be the case.
The instance appeared to have just rebooted out of the blue.
Next I wondered if someone had issued a reboot via the AWS Admin Console or the cli.
I did not know of any easy (any really) way to check past usage so I filed a support request and the response was that they had had a hardware failure causing our instance to restart.
While waiting for their reply I had the opportunity to check their forums and ran across CloudTrail.
CloudTrail is the AWS auditing service that, when enabled, will audit (timestamp and who) every AWS API usage and keeps the audit logs in an S3 bucket that you designate.
You do have to enable the service to get it started but once you do it can make you aware of what is going on (and went on) in your account.
There is not cost for the service other than the S3 space where the logs are kept.
This is useful in a number of ways including knowing who did what and being able to correlate that with your cost data.
For example, if you have a team of developers and one of then is generating higher EC2 costs than the others it might be due to an inefficient use of the EC2 and useful to pursue the cause.

Another is helping to determine why some unexpected event occurred.
Along this same line it is worthwhile to point out that using a cloud provider can make you complacent in thinking that their compute resources are always up.
Realistically you have to be aware that any computer related resource can fail at any time and your architecture/system needs to take that into account.
If you have a service up on one EC2 instance you should be aware that it could go down unexpectedly at any time.
If you do not have a failover plan (that you know actually works) you may find that your service is offline and losing money.
CloudTrail can help you determine why it went offline but hopefully your other EC2 instance has taken up the load and the audit trail is an investigation only when you have the time.

I'll be looking at correlating the CloudTrail logs with the detailed cost report at some point and will pass along what I learn.



