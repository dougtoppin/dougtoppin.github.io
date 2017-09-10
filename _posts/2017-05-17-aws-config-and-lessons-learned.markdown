---
layout: post
title: "AWS Config and Lessons Learned"
date: 2017-05-17 18:43
comments: true
categories: [aws]
description: Use the AWS Config service to detect unexpected resource usage (or pay the price).
keywords: aws
---
Lesson learned today that taught me the value of using the AWS Config service to check for expected resource usage.
I inadvertently launched an ec2 c4.large instance yesterday while experimenting with the Batch service (it is surprisingly not explicit about an impending launch).
I noticed the unusual instance type running and thought it had been started by someone else in my group.
They also had noticed it and thought I had launched it. 
I asked about it and we realized neither of us had intentionally launched it.
That caused me to add a rule to the Config service to consider any type outside the usual 3 types that we launch to be noncompliant in the config report.
I have not yet come up with a way to prevent the launch in the first place but that is on my list (IAM policy coming).
Another interesting part of this is that since it was a managed service the user was listed as the root account even though it was due to me.
This was because Batch created an autoscaling group of 0-1 with a desired state of 1 by default so be aware that ASGs might launch as well (particularly out of the normal workday).
Note that some instances can run $13/hour. Also pay attention to what your ec2 account limits are.
If they are in the 10s/100s you could run up a pretty good bill unexpectedly.
You cannot set limits by individual instance types (at least directly).
Now that I am much more familiar with Config I expect to be using it quite a bit more.