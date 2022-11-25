---
layout: post
title: "Amazon EventBridge Scheduler and DST Support"
date: 2022-11-24 12:00
comments: true
categories: [blog]
description: Amazon EventBridge Scheduler
keywords: aws eventbridge scheduler
---
I needed to update an AWS CloudWatch event rule in a SAM project which I have to do twice a year because of DST.
The rule is to execute a Step Function every work day at 3 particular times.
Because of DST changes during the year I had to adjust the start time by adding or subtracting an hour.

I decided to instead use the Amazon EventBridge Scheduler which supports DST.
#serverlessland has an example of exactly what I needed at https://serverlessland.com/patterns/eventbridge-schedule-to-lambda

The one change that I had to make to the example template was the cron schedule and timezone that I wanted it to use.

The result looks like this:

```  TestScheduler:
    Type: AWS::Scheduler::Schedule
    Properties: 
      Description: >
        Example of using the EventBridge Scheduler with local timezone support
        provided by the ScheduleExpressionTimezone attribute.
      FlexibleTimeWindow: 
        Mode: 'OFF'
      Name: 'TestEventBridgeScheduler'
      # every workday at 4:00, 4:15, 4:30pm ET
      ScheduleExpression: 'cron(0,15,30 16 ? * MON-FRI *)'
      ScheduleExpressionTimezone: 'America/New_York'
      State: 'ENABLED'
      Target: 
        Arn: !GetAtt ScheduledLambdaFunction.Arn
        RoleArn: !GetAtt MyFirstScheduleRole.Arn```

This will now work correctly for the entire year without me having to make my twice a year change.

The EventBridge Scheduler documentation is at https://docs.aws.amazon.com/eventbridge/latest/userguide/scheduled-events.html

AWS announcements can be found at https://aws.amazon.com/new
