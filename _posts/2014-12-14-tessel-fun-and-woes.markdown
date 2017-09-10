---
layout: post
title: "Tessel fun and woes"
date: 2014-12-14 18:14
comments: true
categories: 
---
I recently bought a Tessel [https://tessel.io/](https://tessel.io/) and have spent a few hours this weekend doing a little more with it beyond just the basic few starter projects.
While it has worked reasonably well enough standalone I've been having regular trouble with my wifi connectivity.
I have an Apple TimeCapsule wifi network and have been completely unsuccessful connecting to it from the Tessel.
As a fallback measure I plugged an Airport Express wifi router in and was able to connect to it with no trouble yesterday but today have had no success with that.
I am guessing that the TimeCapsule issue may have to do with its dual band configuration but am not positive and I do not want to make any configuration changes to it.
I was hoping that the Airport Express would eliminate any wifi issues but am guessing that the issue with it today has to do with the signal strength today but am not sure about that either.

The project that I am working on is to collect environmental data consisting of temperature, humidity and ambient light and sound and store the values into a cloud.
My first choice for that was using the AWS DynamoDB but unfortunately the Tessel is unable to use the AWS JavaScript SDK.
I switched to use KeenIO [https://keen.io/](https://keen.io/)and was able to get that to work yesterday and collected a number of readings and was able to save them.

I was hoping that this would turn out to be something that I could experiment with off and on but unfortunately that is turning into a bigger time user than I had hoped so far.

More to come on this.
