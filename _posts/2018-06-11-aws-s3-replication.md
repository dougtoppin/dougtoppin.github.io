---
layout: post
title: "Using CloudFormation to Configure AWS S3 Bucket Replication"
date: 2018-06-11 15:15
comments: true
categories: [blog]
description: AWS S3 buckets can be replicated to another region. This is an example of how to do that using CloudFormation.
keywords: aws s3
---
AWS S3 buckets are highly reliable but it is worthwhile to be aware that the contents of a bucket are stored in a single region.
Because of this there is always a risk that a regional outage might result in bucket contents not being available to other regions.

A way to resolve this is to use the AWS S3 Cross Region Replication support in S3.
This will cause any object stored in a bucket that has been so configured to be replicated to a bucket in a different region.

An example of doing that using CloudFormation to create the 2 different buckets can be found at [https://github.com/dougtoppin/example-aws-s3-cross-region-replication](https://github.com/dougtoppin/example-aws-s3-cross-region-replication)

An example of where this might be helpful is in disaster recovery plans where it is necessary to ensure that bucket data is always available even in a regional outage situation.
