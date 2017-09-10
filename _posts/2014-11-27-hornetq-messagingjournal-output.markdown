---
layout: post
title: "JBoss Fuse Service Works and HornetQ messagingjournal output"
date: 2014-11-27 22:07
comments: true
categories: 
---
Red Hat JBoss Fuse Service Works (FSW, `jboss-fsw-installer-6.0.0.GA-redhat-4.jar` version) uses HornetQ as a JMS message broker by default.
The JBoss admin console can be used to gather information about the state of the JMS resources for a few items such as message counts but it is not an exhaustive set of what is actually available.
However the specific details of the messages are not available via the admin console.
One example of those details include scheduled future delivery information for a message such as that associated with the _HQ_SCHED_DELIVERY property.
Messages that have a future delivery scheduled are not actually in the queue in memory but can be found stored in messagingjournal files contained in `jboss-eap-6.1/standalone/log/data/messagingjournal/`.
The journal files are not in an easily readable textual format so a tool is required to access them.
A tool can be a shell script implemented using the HornetQ jar files found in the FSW distribution.

Below is an example of this script.
Note that the referenced jar files should be under the `$JBOSS_HOME/modules/system/layers/base` directory.
Different versions of FSW may have different versions of the jar file names but determining the correct ones for your distribution should not be difficult.


    #!/bin/sh
    # hq-dump
    # dump hq journals

    JBOSS_HOME=~/jboss-eap-6.1

    DATA=$JBOSS_HOME/standalone/data

    cd $JBOSS_HOME/modules/system/layers/base

    java -cp org/hornetq/main/hornetq-server-2.3.5.Final-redhat-2.jar:org/hornetq/main/hornetq-commons-2.3.5.Final-redhat-2.jar:org/hornetq/main/hornetq-journal-2.3.5.Final-redhat-2.jar:org/hornetq/main/hornetq-core-client-2.3.5.Final-redhat-2.jar:org/jboss/logging/main/jboss-logging-3.1.2.GA-redhat-1.jar:org/jboss/netty/main/netty-3.6.6.Final-redhat-1.jar:netty-3.2.6.Final.jar:hornetq-logging-2.2.13.Final.jar  org.hornetq.core.persistence.impl.journal.PrintData $DATA/messagingbindings $DATA/messagingjournal

Note that the line starting with `java` is one long line without embedded newlines and the arguments are the jars to add to the classpath, the location of the messagingbindings and messagingjournal files.

Running this script should output the contents of the messaging journal files in readable form.
Each record will be on a new line prefixed by something similar to `recordID=7236283;` with the recordID identifying a specific JMS message along with all of the specifics associated with the message (but without the actual content of the message).

An example of one record of output using this method follows.

    recordID=7236299;userRecordType=32;isUpdate=true;AddRef;QueueEncoding [queueID=23]
    
    recordID=7236299;userRecordType=36;isUpdate=true;ScheduledDeliveryEncoding [scheduledDeliveryTime=1417144050666]
    
    recordID=7236319;userRecordType=31;isUpdate=false;Message(messageID=7236319;properties=[jmsredelivered=false,_HQ_SCHED_DELIVERY=1417144055726,jmsdeliverymode=2,jmspriority=7,jmsxdeliverycount=2,jmsexpiration=0,jmsmessageid=ID:fe8d2bc0-76aa-11e4-809e-875829c5b084,jmstimestamp=1417143751514,org_DOT_switchyard_DOT_messageId=ID-dougs-mbp-5-home-53592-1417143558533-5-92,breadcrumbid=ID-dougs-mbp-5-home-53592-1417143558533-5-79,__HQ_CID=01083de6-76ab-11e4-809e-875829c5b084,#properties = 11] - ServerMessage[messageID=7236319,priority=4, bodySize=6400,expiration=0, durable=true, address=jms.queue.myqueuename,properties=TypedProperties[{jmsredelivered=false, _HQ_SCHED_DELIVERY=1417144055726, jmsdeliverymode=2, jmspriority=7, jmsxdeliverycount=2, jmsexpiration=0, jmsmessageid=ID:fe8d2bc0-76aa-11e4-809e-875829c5b084, jmstimestamp=1417143751514, org_DOT_switchyard_DOT_messageId=ID-dougs-mbp-5-home-53592-1417143558533-5-92, breadcrumbid=ID-dougs-mbp-5-home-53592-1417143558533-5-79, __HQ_CID=01083de6-76ab-11e4-809e-875829c5b084}]]@1183324433

There is a plethora of information in the output that includes property values as well as numerous other fields.

There may be better methods for accomplishing this but this works reasonably well enough.

A better version of this script can be found at [https://github.com/dougtoppin/hornetq](https://github.com/dougtoppin/hornetq)

I found some of the details above from this gist [https://gist.github.com/aparnachaudhary/8029914](https://gist.github.com/aparnachaudhary/8029914).

