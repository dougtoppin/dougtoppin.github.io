---
layout: post
title: "OpenShift and build error New (InvalidOutputReference)"
date: 2017-01-09 20:43
comments: true
categories: [openshift, paas]
description: A cause of the OpenShift build error InvalidOutputReference might be not having created an imagestream.
keywords: openshift, openshiftv3

---
I had a recent experience with troubleshooting a build problem with something in an OpenShift v3 project that I wanted to pass along.
I did a number of searches on the error (InvalidOutputReference) and did not find the lack of an existing imagestream as a possible cause.

If your build status output includes the following

    "New (InvalidOutputReference)"

It may mean that you need to create an image stream before the starting build with this

    $ oc create is myapplication

It is possible that the build has failed but OpenShift will not realize it and will continue saying that the build is in progress.

If your build configuration has a section like this:

    spec:
      nodeSelector: null
      output:
        to:
        kind: ImageStreamTag
        name: myapplication:latest

Then you should be able to do the following and get back an imagestream.

    $ oc get is myapplication

If you can't that may mean that you need to first create the image stream. Note that if your build is pulling from an upstream image it is possible that an imagestream is being created automatically.

OpenShift is a powerful container orchestration (and more) environment.
You can find out more about the community version at [https://www.openshift.org/](https://www.openshift.org/) and the Red Hat supported verson at [https://www.openshift.com/](https://www.openshift.com/)
