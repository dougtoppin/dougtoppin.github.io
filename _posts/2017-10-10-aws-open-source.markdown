---
layout: post
title: "Do you run run open source utilities/containers without controlling what they can do?"
date: 2017-10-10 16:29
comments: true
categories: [blog]
description: Do you run open source utilities using your AWS admin privileges?
keywords: aws oss opensource security
---
Something that I've been wondering about for a while is how often I run tools or open source software utilities with a shell context that has access to my AWS account permissions.

What I mean by that is if you have a *~/.aws/config* file with a *[default]* block in it and the access and secret keys are populated in that section do you ever consider those being available when you run commands?
If the tools you are running were built and linked with an AWS SDK what prevents them from doing any nefarious with whatever permissions are allowed?

Is it a good idea to only run tools you are not intimately familiar with using a docker container that does not have access to your host or aws configuration?
containers inherently provide significant protection by restricting what is being run to a very limited set of actions.

An alternative is not having a default stanza or at least have a default with minimal perms if any.
This would force you to use a *--profile* argument on every aws cli action but would reduce the risk of anything bad happening to your account.

More to come on this subject.
