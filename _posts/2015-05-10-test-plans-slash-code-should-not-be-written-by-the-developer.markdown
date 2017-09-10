---
layout: post
title: "Test plans/code should not be written by the developer"
date: 2015-05-10 11:54
comments: true
categories: 
---
A recent experience (aka lesson re-learned) has once again taught me that when you have to make code changes in a hurry two different people should change the code and plan/write test cases.
The experience was a production issue involving some logic.
We realized what the issue was and a code change was made along with roughing in a few JUnit test cases.
The unit tests worked fine and we were in a hurry to get the mod to QA.

The red flag in the above is high lighted by "in a hurry".
The new build went to QA and after a couple of hours we heard that it was not working.
We checked the unit tests and they were passing without any issue.
After some discussion with QA we realized that the issue was that the new code and unit test code had the same very small bug in them so the unit tests would pass even though the logic issue was still there.

The main point of this is that when you are in a hurry at least a desk check by someone else acting in an independent role might prevent you from messing up the hurry.
