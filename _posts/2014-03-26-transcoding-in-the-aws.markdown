---
layout: post
title: "Transcoding in the AWS"
date: 2014-03-26 20:40
comments: true
categories: 
---
Amazon presents the perfect platform for compute, storage and digital data delivery. The storage and delivery aspect can be applied to media files such as video along with many others. For video it is not unusual that there is a need to tailor the video for the device it is being delivered to. An example of this is the form factor, display size or the bandwidth available for communicating with the device.
The original video file may be high definition implying that is likely very large and trying to push it to a small phone or tablet display may lead to an poor experience for the user. 
While you can perform conversion functions to the media filesd to provide a more acceptable level of performance to your users that will require some technical knowledge, storage and management of the original and new files.
The Amazon Elastic Transcoder service can be used to transcode media files into formats that are appropriate for a variety of devices. The transcoding service uses S3 buckets for file input and output. This enables you to maintain an archive bucket for your original media and then use the automated functions of the transcoding service to produce each of the output files that are appropriate for your users.
Your website/delivery service can then be configured to determine the most appropriate file format to send to the user and retrieve it from the associated bucket that the transcoding service sent the converted files to.
