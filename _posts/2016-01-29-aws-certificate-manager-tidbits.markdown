---
layout: post
title: "AWS Certificate Manager tidbits"
date: 2016-01-29 21:57
comments: true
categories: [aws]
description: Information about using the AWS Certificate Manager service
keywords: aws

---
Amazon AWS recently enabled an ssl certificate manager service.
This service makes the process of creating and using SSL certificates much easier than the more manual methods previously required.

There are several sites and blogs that have been published explaining how to use this service that I have found useful.

They include the following

* [https://dpron.com/ssl-with-aws-certificate-manager/](https://dpron.com/ssl-with-aws-certificate-manager/)

I wanted to pass along any useful pieces of information about my own experience with the service.
I am still new to it but one thing to be aware of being using it is that to request a certificate AWS will send emails to the following addresses associated with your domain to ensure that you actually own the domain.
Those addresses include the following where `@yourdomain` is replaced with your domain.

* hostmaster@yourdomain
* administrator@yourdomain
* webmaster@yourdomain
* postmaster@yourdomain
* admin@yourdomain

It is useful to ensure that you have set up those addressess with your domain registrar before starting the certificate request so that the process moves smoothly.
It is also a good idea to test and confirm that the addresses that you set up work correctly if they did not already exist.
