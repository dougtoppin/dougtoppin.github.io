---
layout: post
title: "Effective Logging For Consumption"
date: 2015-12-11 11:21
comments: true
categories: [software, logging]
description: Examples of good and bad log statements
keywords: software, logging, splunk

---
Log aggregators such as [Logstash](https://www.elastic.co/products/logstash) and [Splunk](http://www.splunk.com/) provide great benefit in terms of monitoring and awareness of what a system is doing and how it is performing.
Associated with that comes alerting when issues or trends are detected as well as analytics such as a change in some normal pattern.

For aggregators to be effective the log statements written during development need to be thought through and planned so that they provide the base data values that can be later easily consumed and processed.

An example of a useful log pattern would be

    timestamp loglevel [class] message="processing values", requestsToExternalService=“15”, durationOfRequests=“230”, successfulResults=“12”, failedResults=“3”, transactionId=“xxx”, externalServiceProvider=“serviceA"
    
With the above format a logging aggregator can easily find and graph rates of requests to a particular service provider.
It can also have line graphs showing total request count along with a breakdown of successful and failed counts.
Including the duration means that normal patterns can be seen and changes in trends are visible and alerting can be configured for limits that may indicate an issue with the provider interface.
Including a transactionId that is repeated for each related message logged during a transaction enables identifying specific requests or activities that are of concern or later tracing the path of some event that occurred.
In general using key value pairs for values is much easier to consume than a long string that has to be parsed to extract desired fields.

The key element for all of this is that during development if the above values are not stipulated as a part of logging the developer may not have the values available in the code or not plan for a single statement that contains all of them.
Instead a developer (who may not be thinking of the value of the logging to operations later) may log the values across several statements making it more difficult for the aggregator to collect and correlate them or worse not log them at all.

If poor logging practices make it into a production environment it becomes difficult to later improve them because the logging and alerting system may already be configured for what exists.
Making a change to an existing log statement may cause a subtle issue or even a breakage in altering later.

As usual, anything undesirable that makes it into production becomes much more expensive to correct or improve later.

An example of the above pattern done poorly across multiple statements might look like the following:

    timestamp loglevel [class] message="processing values for transaction xxx"
    timestamp loglevel [class] message="failed count 3"
    timestamp loglevel [class] message="successful requests 12"
    timestamp loglevel [class] message="serviceA"
    
As can easily be seen the above series of statements (that may have other activities in between them) have to be collected, parsed and then potentially correlated.

The concept of Monitoring Driven Development should be followed where software logging is planned in a way to facilitate consumption by monitoring and log aggregation systems later.
The software will be in use for much longer than it took to develop and test it.

    

