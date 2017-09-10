---
layout: post
title: "Thoughts on data access and monitoring"
date: 2017-07-13 20:21
comments: true
categories: [data]
description: The importance of controlling access to data cannot be overstated.
keywords: breach
---
In reading about the recent Verizon subscriber data breach I recognize even more the importance of monitoring access and actions on data in cloud accounts.
By that I mean in the Verizon case a contractor was apparently able to access and download a large amount of subscriber data.
Then that data was put into a public AWS S3 bucket.
This demonstrates the importance of several architectural aspects of your system including the following

* encrypt data at rest and restrict key access
* enable access to critical data sets by IAM role
* use API activity monitoring to note unusual accesses even by allowed accounts, for example "account x just did a very large query or a large number of queries", this might be done via AWS resources (CloudWatch for example) or external tools such as a log aggregation system that can detect and alert
* configure temporary roles or credentials to allow access to keys or data
* scan your account resources for things like public S3 buckets on a regular basis
* have a plan and communication or reporting channels in place to react quickly, in the Verizon case it appears that a number of days passed after detection before anything response was made

Each of these actions take planning in advance and effort but the cost of not doing them or missing one can be much greater in actual labor, reputation or goodwill down the line.
