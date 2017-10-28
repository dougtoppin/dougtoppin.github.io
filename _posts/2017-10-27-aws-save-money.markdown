---
layout: post
title: "AWS - Save Some Money"
date: 2017-10-27 22:00
comments: true
categories: [blog]
description: (redux) Do not use bigger instance types than you need
keywords: aws openshift
---
I regularly start EC2 instances in the AWS and use the spot market whenever I can.
Typically this results in reduced costs of at least 25% and frequently much more than that.
Lately I've been launching an instance to do some OpenShift work (using `oc cluster up`).
Generally I've used a c4.2xlarge instance with 100 gb attached.
This works very well for my purposes but the spot cost of that instance will range from $0.11 to $0.14 per hour.

While this does not sound like a lot it does add up after a day or two.
I decided to check the cpu utilization of it and it runs less than 20%.
As a result I am trying out the c4.xlarge at around $0.05 per hour (spot).

This looks like the following
```
c4.2xlarge:

$ 0.14*24
$ 3.36

c4.xlarge:

$ 0.05*24
$ 1.20
```

This may not look like a lot but when you do it regularly in your personal account your bill begins to be noticeable.

I am going to do my usual work on the c4.xlarge and if it performs well enough I'll make it a habit.

The key points in this post are to use the spot market if possible and check your instance utilization.
If you can get by with smaller/cheaper then do so.

Don't spend money that you do not have to.

Also, if you want to run OpenShift `oc cluster up` will do so all in containers.
Take a look at [https://github.com/openshift/origin/](https://github.com/openshift/origin/) for details.

To fully provision your instance include the following in the user data at launch.

```
#!/bin/bash
yum update -y
yum install -y mlocate
updatedb
yum install -y git
yum install -y docker
service docker start
sleep 5
usermod -a -G docker ec2-user
sed -i 's/^OPTIONS.*/OPTIONS="--insecure-registry 172.30.0.0\/16 --default-ulimit nofile=1024:4096"/' /etc/sysconfig/docker
service docker restart
sleep 5
cd /tmp/
wget https://github.com/openshift/origin/releases/download/v3.6.0/openshift-origin-client-tools-v3.6.0-c4dd4cf-linux-64bit.tar.gz
gunzip openshift-origin-client-tools-v3.6.0-c4dd4cf-linux-64bit.tar.gz
tar xvf openshift-origin-client-tools-v3.6.0-c4dd4cf-linux-64bit.tar
cp openshift-origin-client-tools-v3.6.0-c4dd4cf-linux-64bit/oc /usr/local/bin/
mount --make-shared /
sed -i.bak -e 's:^\(\ \+\)"$unshare" -m -- nohup:\1"$unshare" -m --propagation shared -- nohup:' /etc/init.d/docker
```

After launch, do the following to get your *cluster* up.

```
/usr/local/bin/oc  cluster up --routing-suffix=`curl http://169.254.169.254/latest/meta-data/public-ipv4`.nip.io --public-hostname=`curl http://169.254.169.254/latest/meta-data/public-hostname`
```
