---
layout: post
title: "AWS Lambda and Static Site Authentication"
date: 2015-07-07 22:33
comments: true
categories: [aws, lambda]
 
---
If you are into the AWS and software system you should get familiar with Lambda.
This is a big step in the direction of having your NodeJS and Java code hosted by AWS without you having to run an EC2 instance for it.
This, combined with services like DynamoDB/RDS/S3 and an AngularJS UI hosted on a static site, means that your entire architecture could run without any concern for scaling, redundancy and disaster recovery and significantly cheaper than you having to setup and maintain EC2 instances.
Your operational fixed costs and monitoring related labor drop significantly. Plus, it is pretty cool.

An example is a github repo that I forked and made a few additions to. It is a static site that provides authentication via Lambda and DynamoDB.
You can find it at [https://github.com/dougtoppin/LambdAuth](https://github.com/dougtoppin/LambdAuth) .
I have a few other additions that I am going to make and am going to improve the doc a little but [Danilo Poccia](https://github.com/danilop/LambdAuth) (the original repo) did an excellent job on it.