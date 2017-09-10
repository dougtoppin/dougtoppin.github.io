---
layout: post
title: "OpenSSL bug and be careful with updating sshd on the EC2"
date: 2014-04-08 23:08
comments: true
categories: 
---
Tidbit for anyone updating due to the OpenSSL (heartbleed.com) bug.
Some instructions say to update and then restart impacted services (such as sshd, apache, nginx, mysql, postfix, ...) or rebooting.
Note that the following Red Hat RHEL bug https://bugzilla.redhat.com/show_bug.cgi?format=multiple&id=956531 may ruin your /etc/ssh/sshd_config file causing sshd to not be able to restart so if you reboot the instance without correcting that problem (if it exists) then sshd will probably not be able to start and you will not be able to ssh in (important for your AWS EC2 instances).
I recommend that for your EC2 instances that you update and then try restarting sshd manually to confirm that it is able to start.
