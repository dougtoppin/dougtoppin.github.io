---
layout: post
title: "Tip on uniquely naming your AWS S3 buckets"
date: 2018-06-06 15:15
comments: true
categories: [blog]
description: It is a good idea to name your AWS S3 buckets by including the region they were created in.
keywords: aws s3
---
For files in AWS S3 it is a good practice to include the region name in the bucket names that are being created.
The reason for this is that the S3 namespace is global but the contents are stored in the region that the object was created.
For example, if us-east-1 was down and a failover occurred to us-west-1 the bucket contents that were created in us-east-1 might not be available.
S3 supports a Cross Region Replication configuration setting that will cause the objects stored in a bucket to be replicated to a differently named bucket in another region.

Note that I do not generally see the stipulation "differently named bucket" when I read about this capability.
It will not allow you to replicate to a bucket with the same name in another region because that would result in a namespace conflict.

Because of this it is a good practice to always include the region name in the bucket names that you create.
This facilitates adding cross region replication later if you decide that you want buckets to exist in multiple regions particularly in a DR scenario.

An example of this are the bucket names ```mybucket01-us-east-1``` and ```mybucket02-us-west-1```.
This would allow ```mybucket01-us-east-1``` to be configured to replicate to ```mybucket02-us-west-1```.
