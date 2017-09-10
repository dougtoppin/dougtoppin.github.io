---
layout: post
title: "Quick static site photo gallery"
date: 2014-04-26 21:02
comments: true
categories: 
---
Recently I needed to quickly stand up a photo gallery to show 50 or so event pictures that I had taken over the last few weeks.
I debated various ways of doing this and knew that I wanted it to be a minimal effort exercise.
I decided to do it using an S3 hosted static site.
Since the gallery did not need to have any site editing/uploading type capabilities I went with fgallery (http://www.thregr.org/~wavexx/software/fgallery/).
fgallery will take a set of images in a directory and create the static site pages containing html/css in an output directory that you then upload to your site.
The only issue that I ran into was that fgallery needed a few packages that I did not have installed on my Mac.
I tried using my VirtualBox to start an Ubuntu but had a problem with it and did not want to take the time to troubleshoot that.
Rather than install the packages on my Mac (I already have 3 different package installation systems on it) I fired up an EC2 Ubuntu instance, uploaded the pictures to it and then installed fgallery and the required packages on it.
I used the default args for fgallery and had it generate the site files.
I was using a micro EC2 instance so it took a little longer than I expected for it to process the images but it was probably less than 15 minutes total.
I used the Python simple http server to verify that the resultant site files looked good enough.
I then created an S3 bucket configured for static hosting and uploaded the site files using the awscli s3 copy command.

aws s3 cp dir s3://mybucket --recursive

Once that was done the site was ready.
I had no complaints about fgallery at all.
If you want it up there quick it works.
In general, you can't beat the speed and flexibility of the EC2 for standing up compute resources and the S3 for hosting them.
AWS rules.

