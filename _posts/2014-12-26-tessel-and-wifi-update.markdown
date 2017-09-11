---
layout: post
title: "Tessel And Wifi Update (and Keen.IO)"
date: 2014-12-26 21:24
comments: true
categories: 
---
In my previous post at [http://blog.dougtoppin.name/2014/12/14/tessel-fun-and-woes.html](http://blog.dougtoppin.name/2014/12/14/tessel-fun-and-woes.html) I described how I have been having trouble with my Tessel not wanting to stay connected to my wifi network.
The problem appears to be signal strength related because if I move the Tessel (much) closer to my AirportExpress router it is able to hold the connection.
This is not particularly convenient but at least lets me continue experimentation with it.

Since the current Tessel code is not compatible with the AWS JavaScript SDK I am using [https://keen.io/](https://keen.io/) as the cloud provider to store my data.
That is working well and has given me the chance to learn a little more about Keen.IO which is a data analytics platform so just being used for storage is only an ancillary benefit.
Once you get data uploaded to Keen there is `workbench` function in their web UI which lets you access and examine your data in a variety of ways.

A particularly useful Keen capability is that it also provides an API for access to your data which gives response format options for convenience.
If you are not familiar with Keen.IO I recommend taking a look at it as there are a number of things that be done to any sort of data set that you have and want to glean more information from.


