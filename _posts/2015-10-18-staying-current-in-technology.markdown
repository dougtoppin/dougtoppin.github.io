---
layout: post
title: "Staying current in technology"
date: 2015-10-18 12:39
comments: true
categories: [technology]
description: Staying current in technology using open source software
keywords: technology, github, opensource, learning

---
One of the most challenging aspects of working in software technology is the breadth of what that term actually means. With the plethora of applications, languages, operating systems, frameworks and technologies that exist simply being aware of them can be challenging much less than being proficient in all of them.

Being interested in our field is not enough any longer. Now you have to also allocate the time to read (or listen to relevant podcasts) and actually try out things that you find interesting. I am regularly finding that priorities and reasonable approaches have to be set to learn things. It is not easy to start from scratch in terms of writing software. I generally find that it is much more informative and time efficient to find something that already exists that is associated with what I am interested in and then use that as a starting point.

By far and away GitHub has facilitated/enabled that more than any other resource that I have found. When I want to learn something I almost always start with a GitHub repository search to see if something exists that I can use as a starting point.

A recent example is that I have a WaterRower rowing machine that has an S4 performance monitor with a USB connection. Since just sitting there rowing can be a little monotonous I looked around for software that could talk to the S4 and maybe do something with the data. The only packages that I could find were MS Windows based and would not work on my MacBook Pro so I headed to GitHub to see what I could find.  I found a repo with a NodeJS script that would read data from the S4 but used a serialport package that would not install on my machine when I tried it. I spent an hour or so trying to figure out why and discovered that all I needed to do was update a version number for the serialport package. Once I did that the script worked fine. This also helped me refresh some of my NodeJS knowledge.

Since simply reading data is not all that fun I wanted to do something with it so I decided to modify the script to send the data to a Keen.IO collection. Keen.IO is "a single platform to capture and analyze your data and display it wherever you need it - for your teams and your customers". I have used it in the past and it has worked very well for collecting and displaying data. I had not used Keen in a while so this also helped refresh me a bit.

Had I wanted to start from scratch to connect to and read the S4 data and send it somewhere to be processed it would have taken so much longer to implement that it have would been not have been possible in the 2 hours that I spent doing the above.

The point of this post is that open source provides a tremendous opportunity for learning as well as saving time in actually getting something done when you do not have limitless time (or budget). Also, this was way more fun and interesting than just sitting there rowing.

My WaterRower script can be be found at [https://github.com/dougtoppin/waterrower-s4-keen](https://github.com/dougtoppin/waterrower-s4-keen)
