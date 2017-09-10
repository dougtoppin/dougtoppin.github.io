---
layout: post
title: "Packer and Mac OSX note"
date: 2014-01-01 21:39
comments: true
categories: 
---
I did a little experiementing with Packer (http://www.packer.io/) today on my MacBook Pro and wasted some time before I realized that I was running the wrong build for OSX.
The error that I was getting when I tried to build the example Amazon ami included the following output:

    Build 'amazon-ebs' errored: Error creating temporary keypair:
    .....
    failed to load system roots and no roots provided
    ...
    Builds finished but no artifacts were created.

I was trying my first build using the example at http://www.packer.io/intro/getting-started/build-image.html
After thinking that the error had to do with my secret key I stumbled on this post https://groups.google.com/forum/#!topic/packer-tool/E0u-L52bMBw which included a note about using the amd instead of the i386 build.  I downloaded the amd build and it started working fine.

If you are not familiar with Packer it is a tool that can be used to create machine images such as an Amazon AMI along with others.
Note that if you try out the Amazon image build example it will generate an image, deploy it to a newly created AWS EC2 instance and then terminate (meaning destroy) the image.  If you check your AWS console after this successfully completes you should see an EC2 t1.micro instance entry with the name and tag 'Packer Builder' in a 'Terminated' state.  A primary advantage of Packer is that you should be able to regenerate the image whenever you need it so there is no need to 'stop' it (as opposed to 'terminate').


