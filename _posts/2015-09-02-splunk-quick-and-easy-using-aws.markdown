---
layout: post
title: "Splunk Quick and Easy Using AWS"
date: 2015-09-02 21:59
comments: true
categories: [splunk,logging]
description: Splunk Quick and Easy Using AWS
keywords: splunk, aws, logging

---
I use [Splunk](http://www.splunk.com/) for log aggregation, visualization and analysis and recently had an interesting experience that I wanted to pass along.
For the enterprise server that I use (dev and prod environments) I do not have administrator access so I can't add stuff to it nor change the configuration.
I wanted to try out a plug-in module for it called [REST API Modular Input](https://splunkbase.splunk.com/app/1546/) which adds the ability to collect data from ReST endpoints.

I was going to have to install Splunk and a database for its data but instead found the Splunk AMI in the Amazon AWS Marketplace.
Using that I selected the instance type (m3.medium) that I wanted ($0.07 an hour) and started it up.
Within 5 minutes I was able to get to the Splunk console and then in another 15 minutes I had installed the ReST module and had it collecting weather data from Yahoo.

The Yahoo weather query is

    https://query.yahooapis.com/v1/public/yql?q=select%20*%20from%20weather.forecast%20where%20woeid%20in%20(select%20woeid%20from%20geo.places(1)%20where%20text%3D%22ashburn%2C%20va%22)&format=json&env=store%3A%2F%2Fdatatables.org%2Falltableswithkeys
    
That returns this

    {"query":{"count":1,"created":"2015-09-03T02:15:02Z","lang":"en-US","results":{"channel":{"title":"Yahoo! Weather - Ashburn, VA","link":"http://us.rd.yahoo.com/dailynews/rss/weather/Ashburn__VA/*http://weather.yahoo.com/forecast/USVA0027_f.html","description":"Yahoo! Weather for Ashburn, VA","language":"en-us","lastBuildDate":"Wed, 02 Sep 2015 9:50 pm EDT","ttl":"60","location":{"city":"Ashburn","country":"United States","region":"VA"},"units":{"distance":"mi","pressure":"in","speed":"mph","temperature":"F"},"wind":{"chill":"75","direction":"0","speed":"0"},"atmosphere":{"humidity":"79","pressure":"29.95","rising":"0","visibility":"9"},"astronomy":{"sunrise":"6:37 am","sunset":"7:38 pm"},"image":{"title":"Yahoo! Weather","width":"142","height":"18","link":"http://weather.yahoo.com","url":"http://l.yimg.com/a/i/brand/purplelogo//uh/us/news-wea.gif"},"item":{"title":"Conditions for Ashburn, VA at 9:50 pm EDT","lat":"39.03","long":"-77.47","link":"http://us.rd.yahoo.com/dailynews/rss/weather/Ashburn__VA/*http://weather.yahoo.com/forecast/USVA0027_f.html","pubDate":"Wed, 02 Sep 2015 9:50 pm EDT","condition":{"code":"33","date":"Wed, 02 Sep 2015 9:50 pm EDT","temp":"75","text":"Fair"},"description":"\n<img src=\"http://l.yimg.com/a/i/us/we/52/33.gif\"/><br />\n<b>Current Conditions:</b><br />\nFair, 75 F<BR />\n<BR /><b>Forecast:</b><BR />\nWed - Partly Cloudy. High: 91 Low: 67<br />\nThu - Partly Cloudy. High: 93 Low: 69<br />\nFri - PM Thunderstorms. High: 89 Low: 67<br />\nSat - AM Clouds/PM Sun. High: 85 Low: 60<br />\nSun - Sunny. High: 86 Low: 63<br />\n<br />\n<a href=\"http://us.rd.yahoo.com/dailynews/rss/weather/Ashburn__VA/*http://weather.yahoo.com/forecast/USVA0027_f.html\">Full Forecast at Yahoo! Weather</a><BR/><BR/>\n(provided by <a href=\"http://www.weather.com\" >The Weather Channel</a>)<br/>\n","forecast":[{"code":"29","date":"2 Sep 2015","day":"Wed","high":"91","low":"67","text":"Partly Cloudy"},{"code":"30","date":"3 Sep 2015","day":"Thu","high":"93","low":"69","text":"Partly Cloudy"},{"code":"38","date":"4 Sep 2015","day":"Fri","high":"89","low":"67","text":"PM Thunderstorms"},{"code":"30","date":"5 Sep 2015","day":"Sat","high":"85","low":"60","text":"AM Clouds/PM Sun"},{"code":"32","date":"6 Sep 2015","day":"Sun","high":"86","low":"63","text":"Sunny"}],"guid":{"isPermaLink":"false","content":"USVA0027_2015_09_06_7_00_EDT"}}}}}}

Splunk collects and keeps that result and polls at whatever interval you need.

I then used this simple query to see the data

    host="myhosname"| timechart avg("query.results.channel.item.condition.temp")
    
     
That produced a view that looked like [Splunk Weather](https://cloud.githubusercontent.com/assets/1274131/9649271/a79c73ea-51c0-11e5-9050-ba5729b346fc.jpg)

I was very impressed with how quickly I was able to select and start the AMI and the fact that it was ready to go in that it had a running Splunk server and a MongoDB on the same instance to hold the data.

One of the main benefits of using Splunk is that you can use the query results to select fields of interest and do something useful with them without having to be an expert.
I have used a Logstash stack (Logstash, redis, ElasticSearch, Kibana) in the past but setting it all up yourself can take a while and involve a little trial and error.

The Splunk AMI did exactly what I needed in a very short period of time and I was able to do some useful work.
The other nice thing about the AWS experience is that when I am done with it I can terminate it and hit the sack.

