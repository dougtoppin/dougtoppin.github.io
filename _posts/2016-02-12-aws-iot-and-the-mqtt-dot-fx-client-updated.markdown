---
layout: post
title: "AWS IoT and the MQTT.fx Client Updated"
date: 2016-02-12 19:38
comments: true
categories: [aws, iot, mqtt]
description: AWS IoT and the MQTT.fx Client
keywords: aws, iot, mqtt, mqtt.fx

---

In the previous post [http://blog.dougtoppin.name/aws/iot/mqtt/2015/10/09/aws-iot-and-the-mqtt-dot-fx-client.html](http://blog.dougtoppin.name/aws/iot/mqtt/2015/10/09/aws-iot-and-the-mqtt-dot-fx-client.html) I passed along a few tidbits about using the MQTT client with the AWS IoT service.

Since then both the AWS IoT service and the MQTT client have been updated.
I decided to do an updated post with any new info.
The AWS IoT configuration pages have noticeably changed.

The current MQTT client can be found at [http://www.jensd.de/apps/mqttfx/1.0.0/](http://www.jensd.de/apps/mqttfx/1.0.0/).
There are a few visible differences in the client configuration.

The IoT resources main panel now looks like [this](https://cloud.githubusercontent.com/assets/1274131/13024421/9609c614-d1c2-11e5-8725-f3f160c551f0.png).

The certificate resource page now looks like [this](https://cloud.githubusercontent.com/assets/1274131/13024483/59dd41d8-d1c3-11e5-896f-fb37ef5e16fe.png) and the downloads will save as files that help with identifying which they are used for.

The cert names will appear something like these

    xxx-certificate.pem.crt
    xxx-private.pem.key
    xxx-public.pem.key


In the previous post I had to replace newline characters in the cert files but this time I did not and was able to use them as is.

The MQTT client connection settings page will look something like [this](https://cloud.githubusercontent.com/assets/1274131/13024605/04eb32d2-d1c5-11e5-8bbc-1b846778754f.png).

The root-cert can be found in the AWS IoT document [here](https://cloud.githubusercontent.com/assets/1274131/13024615/4b4944e4-d1c5-11e5-82fc-e8def10ff09c.png).

The pub/sub functions in the MQTT client worked without any trouble.
The `Log` tab in the client can provide useful information if you run into any trouble.
If there are any connection issues the cause should appear in the Log.
