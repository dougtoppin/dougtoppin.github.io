---
layout: post
title: "AWS IoT and the MQTT.fx Client"
date: 2015-10-09 08:23
comments: true
categories: [aws, iot, mqtt]
description: AWS IoT and the MQTT.fx Client
keywords: aws, iot, mqtt, mqtt.fx


---
During the AWS re:Invent 2015 conference their new [IoT](https://aws.amazon.com/iot/) service was announced.
This service facilitates the ingestion of a large amount of data from numerous devices that may be sporadically connected to the Internet.

I tried out the AWS tutorial and wanted to pass along a new notes.

I had some trouble installing an MQTT client on my MacBook Pro and was eventually able to get the MQTT.fx client dmg working from [http://www.jensd.de/apps/mqttfx/0.0.18/](http://www.jensd.de/apps/mqttfx/0.0.18/).

I had not used that client before so I had to experiment a little with which cert file to put where.

A screenshot of the settings that I used is at [MQTT.fx and AWS IoT settings](https://cloud.githubusercontent.com/assets/1274131/10393719/5b5513d6-6e60-11e5-8d97-a296e0f3e40a.png)

The cert files that you download may contain `\n` in a number of lines and you should replace those with newlines.
Initially I had only noticed and replaced them after the `CERTIFICATE-----` lines and could not get a client to connect.
Once I replaced all of them (the pem file contents should look like square blocks of text) I got it to work.

At this point you can have your MQTT client subscribe to a topic.
The MQTT.fx subscribe window looks like [this](https://cloud.githubusercontent.com/assets/1274131/10394310/4e946ef4-6e64-11e5-82a6-c3854006078e.png)

Once you are subscribed then you can publish messages to that topic.
The MQTT.fx publish window looks like [this](https://cloud.githubusercontent.com/assets/1274131/10393947/e6cd201a-6e61-11e5-994f-073735f3de69.png)

Once I had the client working I was able to publish a number of messages and see them in the subscribe window which looks like [this](https://cloud.githubusercontent.com/assets/1274131/10393973/08057192-6e62-11e5-8869-6efbf6268308.png)

Next I wanted to try out the new CloudWatch dashboards and created a dashboard.

I selected the IoT metrics from [here](https://cloud.githubusercontent.com/assets/1274131/10394160/39859f16-6e63-11e5-8741-c62662170983.png)

Then I picked the specific ones that I wanted to graph from [here](https://cloud.githubusercontent.com/assets/1274131/10394175/5919318a-6e63-11e5-8734-76331fd7e388.png)

That gave me a dashboard that looked like [this](https://cloud.githubusercontent.com/assets/1274131/10394192/721b2d78-6e63-11e5-9ccf-932f21d34399.png)

The IoT service is going to be an exciting means of collecting, processing and analyzing data from many different devices.

