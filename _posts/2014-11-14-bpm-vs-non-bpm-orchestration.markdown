---
layout: post
title: "BPM vs non-BPM orchestration"
date: 2014-11-14 21:33
comments: true
categories: 
---
After experiencing the repercussions of a prior decision to use a Camel route for orchestrating a number of steps in a business process as opposed to using a Business Process Management (BPM) system I wanted to pass along a few observations (aka Lessons Learned).

While development may proceed more quickly initially (because the time required to learn the BPM system is avoided) the subsequent phases of the project may suffer and require more effort.

Areas of inceased effort will include additional logging in the route to note the stage of the process, additional logging aggregation system effort to consume the log entries and new process error handling code.
When debugging or trouble shooting during test phases the logging will have to include information that would have been available via the BPM system such as where in the process a failure may have occurred, what state the process is "stuck" in, a likely easier means of manual intervention (via the BPM UI) in correcting the request that is causing the issue and so on.
