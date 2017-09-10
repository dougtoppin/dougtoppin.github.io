---
layout: post
title: "Tessel and NodeJS for Fun"
date: 2014-12-08 10:41
comments: true
categories: 
---
Recently I ran across the [Tessel](https://tessel.io/) which is a fun hardware platform that is NodeJS (Javascript) compatible.
This means that you can write some NodeJS code to perform a variety of functions on the Tessel  using just the board itself or using modules that are plugged into it.
There are a number of modules that can collect environmental data (temperature, humidity, light and sound for example), control an external servo and interface with BlueTooth and IR (infrared) devices.
The Tessel can support up to 4 modules plugged into it at once so your code can do all sorts of useful things.

My first project (available at [https://github.com/dougtoppin/tessel-lightservo](https://github.com/dougtoppin/tessel-lightservo) was to sample the ambient light sensor and use the servo to move a pointer indicating whether or not the light was on.
This worked very well and required very little code to make it work.
The on/off sign and pointer attached to the servo were just pieces of paper.
Putting my hand over the ambient sensor worked well for triggering the sensor and the pointer would immediately move to the correct position.

One thing to plan for in using the Tessel for something productive is that you should consider how you are going to mount or position it so that any module requiring an external view will work.
By this I mean you might put the Tessel behind a piece of cardboard or in a box that has holes poked through it so that the ambient module can "see" and then also have holes to mount the servo in.
Putting the Tessel and modules in a box or other similar platform will also help keep it from being dropped, bent or otherwise broken if it is just laying on your table or work bench.

I also have an Arduino and have done a couple of small projects with it.
One contrast that I have seen between the Arduino and the Tessel is that a Tessel project tends to take up less desk space.
With an Arduino I have to have a breadboard, resistors and various wires out.
It takes a longer to break down and pack up an Arduino project than it has so far for my Tessel.
I have a small compartmented box for my Arduino and assorted parts and putting it all back in the box can take a few minutes.
The Arduino is more flexible from the perspective of projects that you do do with it but if you are looking for projects where you just write some code to interact with ready to go modules then the Tessel is probably more convenient.

I definitely recommend the Tessel if you like to write some code that can interact with the external world.
My next project is to collect climate data and store in in the cloud (AWS and/or Keen) and will hopefully be posting about this in the near future.


