---
layout: post
title: "AWS Cloud Trail and rate limiting"
date: 2018-07-31 09:30
comments: true
categories: [blog]
description: Check Cloud Trail for errors every now and then
keywords: aws ssm parameterstore
---
It is a good practive to check your Cloud Trail logs every now and then for errors that might be happening in your AWS account.
An example might be if you are using the api and encountering rate limiting related errors.
Athena is a good means of querying CloudTrail records that have been preserved to S3.

An example of using an Athena query for any CloudTrail records that have a non-null error code follows.
In this case an Athena table was previously created for only CloudTrail records during the month of Jul 2018.
This is to reduce the cost of using Athena as it is priced based on the amount of data scanned.
This query also demonstrates how to constrain the query to particular dates in that data set.


```
SELECT eventtime,
        eventname,
        eventsource,
        useridentity.userName,
        errorCode,errorMessage
FROM cloudtrail_logs_2018_07
WHERE errorCode != ''
        AND eventtime >= '2018-07-30T00:00:00Z'
        AND eventtime < '2018-07-31T00:00:00Z'
limit 50;
```
