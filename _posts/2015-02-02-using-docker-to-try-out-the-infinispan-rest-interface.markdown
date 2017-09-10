---
layout: post
title: "Using Docker to try out the Infinispan ReST interface"
date: 2015-02-02 22:16
comments: true
categories: 
---
I regularly run across examples that say things like "configure this the way that you want it, run it and then use our api to do some stuff".
I generally prefer examples that are more specific for at least getting something to work quickly, preferably by doing exactly what the instructions say.
As a result I decided to come up with a working example using Docker of how to use the Infinispan (aka Red Hat DataGrid) cache.

This will (at least should) build a Docker container that contains Infinispan, configures it a little, starts it and then helps you use Postman to put and get via the ReST interface.

If you are interested you can find it at: [https://github.com/dougtoppin/docker](https://github.com/dougtoppin/docker)
