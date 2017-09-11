---
layout: post
title: "JBoss Infinispan metrics exploration using Docker"
date: 2015-05-06 15:27
comments: true
categories: 
---
For anyone who uses JBoss related stuff like Infinispan which is a cache facility built on JBoss (and who wouldn’t be?) you might find the following at least a little interesting.
I’ve needed to do a  little spin up again on the Red Hat Data Grid (which is based on JBoss Infinispan project).
I looked around for some info and found a blog post of mine on the subject of using a Docker image to try out the Infinispan ReST interface.
I just added some more to that on how to take a look at the metrics that Infinispan keeps which is what I need to do.
You can find my original post at [http://blog.dougtoppin.name/2015/02/02/using-docker-to-try-out-the-infinispan-rest-interface.html](http://blog.dougtoppin.name/2015/02/02/using-docker-to-try-out-the-infinispan-rest-interface.html)

What I am doing right now is adding more detail on how to get to the metrics in Infinispan so bop on down into [https://github.com/dougtoppin/docker/tree/master/infinispan/rest](https://github.com/dougtoppin/docker/tree/master/infinispan/rest) to see what I have added.
I will likely be adding a bit more to it so check back at the same Bat Time and same Bat Channel in the near(ish) future.
If you feel like getting your Docker on to try it out then be my guest.
If you have any questions post them and if you want to make it better you probably already know how to do that in Github.
