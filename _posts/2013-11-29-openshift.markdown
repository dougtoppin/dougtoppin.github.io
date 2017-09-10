---
layout: post
title: "OpenShift, oo-install and the AWS"
date: 2013-11-29 13:58
comments: true
categories: 
---
I have a few days off and decided to put some time in with trying out the updated OpenShift oo-install script (found at source/_posts/2013-11-29-openshift.markdown) and use the AWS for it.  My first try was just a quikie (without really reading the instructons).

My experiences follow:
- allocated a micro EC2 RHEL 6.4 instance
- sudo yum update'd it, took at least a couple of minutes (I was surprised at how much was updated)
- sh <(curl -s https://install.openshift.com/)

The instructions say that only ruby, curl and unzip are needed but I immediately got these errors:

* Could not locate puppet... you will need to add a repository that provides this.
* Could not locate dnssec-keygen... try to `yum install` one of:
  - 32:bind-9.8.2-0.17.rc1.el6_4.6.x86_64
    ...
*  Could not locate htpasswd... try to `yum install` one of:
  - httpd-tools-2.2.15-9.el6_1.3.x86_64
    ...
The deployment check was not successful. See above for specific issues.
oo-install exited; removing temporary assets.

To get puppet I followed instructions from http://docs.puppetlabs.com/guides/puppetlabs_package_repositories.html

- sudo rpm -ivh http://yum.puppetlabs.com/el/6/products/x86_64/puppetlabs-release-6-7.noarch.rpm
- enabled the dev repo
- sudo yum install puppet

For the bind error I did:
- sudo yum install 32:bind-9.8.2-0.17.rc1.el6_4.6.x86_64

For http:
- sudo yum install httpd-tools-2.2.15-9.el6_1.3.x86_64

Restarting the oo-install will cause it to discover the previous settings and use them as defaults.

Numerous errors on missing "stuff" appeared so it looks like I need to actually read about it a bit more.

