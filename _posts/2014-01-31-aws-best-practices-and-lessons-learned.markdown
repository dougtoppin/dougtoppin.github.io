---
layout: post
title: "AWS Best Practices (and lessons learned)"
date: 2014-01-31 14:13
comments: true
categories: 
---
Since starting to use the AWS (Amazon Web Services) I've learned a few things that I thought I would pass along as lessons learned.
A few of these have been obvious but others have been from doing something wrong or less optimal and having to go back and redo work or else live with the way it is configured.
There are a variety of areas for this and I'm going to experiment with organizing them a little better but for now I'll just line them up.

## Security Groups

* If you have a number of servers in your system some of them are likely user facing and some are backend.
It might be temping to try to use a single security group for all of them but if you later need to change some accessibility aspect of the user interface (such as IPs that users might come from) you have to either change that port/IP range for all of your servers (because they are all in a single security group) or else make a new security group for just the user facing server(s) and move the instance to that group.
If you enable a port (such as http) across all of your system you may not be using that port on the other servers at that time but you may deploy something in the future that does listen on it which could result in a security risk.
If you decide to move the instance to a new security group there are a few steps involved.
Moving the instance for a non-VPC configuration requires stopping that instance, create an AMI of it and launching that AMI as a new instance with the new security group.
A good practice might be to have a specific security group for each server that is either user (Internet) facing or have some other data interfaces that make it unique from the other backend servers.
Doing this allows you to change who/what can access that server by changing a single security group (and not making an AMI and re-launching).
This can be a time saver if you are not using EIPs (Elastic IPs) because each reboot/launch will get a new IP assignment which may force you to have to update other dependent security groups.

