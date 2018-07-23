---
layout: post
title: "AWS SSM Parameter Store and Rate Limiting"
date: 2018-07-23 09:30
comments: true
categories: [blog]
description: Be aware that the AWS SSM Parameter Store is subject to rate limiting.
keywords: aws ssm parameterstore
---
The AWS Systems Manager (SSM) Parameter Store is a very useful service for storing data in a key value pair structure. Access to the Parameter Store is controlled by IAM allowing fine grain management of who or what applications can get or set data across your account.

A common usage pattern is in centralizing values such as database endpoints, usernames and passwords although the new-ish Security Manager may be a better approach for you to use in your applications for secrets.

Another example of how it can be used is to replace your shell level environment variables with Parameter Store get operations using the AWS cli. Doing this reduces the effort of managing your environment variables in general by only referring to them by name.

A useful tidbit on the Parameter Store is that you can encounter rate limiting if you are sending too many gets/puts to the service. One scenario where this might impact you is if you use CloudFormation to manage your resources. If your CloudFormation templates include gets or puts to the Parameter Store it is possible that you might get a rate limit error if you happen to do too many things at once.

When you plan your CloudFormation templates and orchestration for managing stacks it is worthwhile to be aware that rate limiting is a possibility and therefore staggering some actions might be a risk mitigation for problems later.

Note that the actual rate limit threshold is not a published value. Experimenting with your expected or typical rate of Parameter Store access is a worthwhile activity to make a part of your project plan.
