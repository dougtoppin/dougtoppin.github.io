---
layout: post
title: "AWS SSM and the parameter store"
date: 2017-07-13 20:04
comments: true
categories: [aws]
description: The AWS SSM parameter store facility is an excellent means of storing a retrieving useful things.
keywords: aws,ssm,parameterstore
---
An issue that I regularly encounter is how to store things like passwords and tokens in a manner that allows access to them across ec2 instances and desktops.
One way is to use the AWS SSM parameter store. (admin console->ec2->Parameter Store).
All you need to do is use the 'create parameter' function with a name and value.
Retrieving it will return a json object that includes the value.

I’m trying to get into the habit of putting values that I typically save in env vars to instead be in the parameter store.
This gives a single location for values that can have strict access control if need be.
Note that this does mean that you need to have connectivity to your AWS account from wherever you are intending to use this (meaning no offline access).

Accessing it via the cli is then done like this:

    $ aws ssm get-parameters --names "test-parameter-1"
    {
        "Parameters": [
        {
            "Name": "test-parameter-1",
            "Type": "String",
            "Value": "test value 1"
            }
        ],
        "InvalidParameters": []
    }

The ```query``` argument can be used to parse out specific values like this

    $ aws ssm get-parameters --names "test-parameter-1" --query "Parameters[0]"."Value"
    "test value 1"

If you need additional flexibility in parsing json you can use the ```jq``` tool.
An example of parsing a specific value using jq follows

    $ aws ssm get-parameters --names "test-parameter-1" | jq .Parameters[].Value
    "test value 1"

Finding what parameters are available can be done like this:

    $ aws ssm describe-parameters
    {
        "Parameters": [
        {
            "LastModifiedDate": 1499869122.618,
            "Name": "test-parameter-1",
            "Description": "experimenting with parameter store stuff",
            "Type": "String",
            "LastModifiedUser": "arn:aws:iam::xxx:user/xxx"
            }
        ]
    }

To just get a simple list of names use the following with ```query``` describing what you want.

    $ aws ssm describe-parameters --query 'Parameters[].Name'
    [
    "test-parameter-1",
    "test-parameter-2"
    ]

Creating a parameter via the aws cli would look like this

    $ aws ssm put-parameter --name test-parameter-2 --type String  --value test-value-2 --overwrite

Using ```--overwrite``` is required if you are replacing an existing value but it can be used for an initial value as well.
